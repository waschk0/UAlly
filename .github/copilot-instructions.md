# Copilot instructions for UAlly

## Build, test, and lint

The repository contains separate frontend and backend TypeScript projects. Their `package.json` files are ignored and are not present in the checkout, so use the package manifests supplied by the local development setup.

### Frontend

Run commands from `frontend/`:

```bash
npm install
npm start
npm run build
npm test
```

For a non-interactive test run, use:

```bash
npm test -- --watchAll=false
```

To run one Jest test file:

```bash
npm test -- --runTestsByPath src/path/to/file.test.tsx --watchAll=false
```

No frontend test files or separate lint configuration are currently tracked. Create focused tests alongside the component or worker they cover when adding behavior.

### Backend

Run commands from `backend/`:

```bash
npm install
npm run dev
npm run compile
```

The documented development script uses a TypeScript hot-reload workflow; `compile` emits JavaScript under `backend/build/`. No backend test or lint command is documented or tracked.

The backend listens on port `8080`, and the frontend API client uses `http://localhost:8080` from `frontend/src/config.ts`. The frontend README also documents port `8080`; treat the root README's `3000` reference as stale unless the local script configuration says otherwise.

## Architecture

- The frontend is a Create React App-style React 18 application. `frontend/src/index.tsx` mounts `BaseLayout`, which selects views in `frontend/src/components/BaseLayout.tsx` using the `currentView` value.
- `frontend/src/state.ts` is the application state coordinator. It owns authentication state, the current user/list/task, collections of categories/lists/tasks, modal state, and mutation methods. Those methods call frontend `Worker` classes and refresh the affected collection after successful mutations.
- `frontend/src/Users.ts`, `Categories.ts`, `List.ts`, and `Task.ts` are the HTTP boundary. Each worker uses Axios and the shared `config.serverAddress` to call the backend REST endpoints. Keep endpoint changes synchronized between these workers and `backend/src/main.ts`.
- The backend entry point, `backend/src/main.ts`, creates the Express app, enables JSON parsing and permissive CORS, serves a static client path, and defines routes grouped by users, tasks, categories, and lists. Routes instantiate the corresponding table worker and return its result.
- `backend/src/tables/Users.ts`, `Tasks.ts`, `Categories.ts`, and `Lists.ts` contain both the domain interfaces/enums and SQLite persistence workers. Each module opens `./db/db.sqlite` relative to the backend process working directory, so run the backend from `backend/` and preserve that database location.
- The SQL files in `backend/src/tables/` describe the SQLite tables: users own categories and lists, lists contain tasks, and IDs are auto-incremented. Keep TypeScript field names and SQL column names aligned, including the existing casing (`users` versus `Categories`, `Lists`, and `Tasks`).

## Repository conventions

- Add or change an API operation in all three matching places: the backend route in `backend/src/main.ts`, the backend table `Worker`, and the frontend Axios worker/state call site.
- Preserve the existing request shape and route style: collection reads use `GET` with IDs in the path, creates/updates use `POST` with JSON bodies, and deletes use `DELETE` with IDs in the path.
- Frontend views receive the shared state object through props and invoke its bound methods rather than maintaining a second application-wide store. After a mutation, refresh the relevant list from the API instead of manually guessing the resulting collection.
- Reuse the domain interfaces and enums exported by the existing worker/model modules (`IUser`, `IList`, `ITask`, `ICategory`, and their state/type enums) when crossing component or API boundaries.
- Keep database access in the table workers and use SQLite parameter placeholders for new queries. Do not put SQL in Express routes or React code.
- The backend expects `backend/server/serverInfo.json` to exist at runtime because `serverInfo.ts` reads it during module initialization. Keep SMTP credentials out of source control and use a local configuration when developing email-related behavior.
