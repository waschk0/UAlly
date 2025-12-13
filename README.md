# UAlly - Task Management Application

A full-stack task management application built with React and Node.js, designed to help users organize their tasks, lists, and categories efficiently.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Running the Application](#running-the-application)
- [API Endpoints](#api-endpoints)
- [Authors](#authors)

## 🎯 Overview

UAlly is a comprehensive to-do list application that allows users to:
- Manage personal and university-related tasks
- Organize tasks into lists and categories
- Track progress with an intuitive interface
- Secure user authentication and profile management

## ✨ Features

- **User Authentication**: Secure registration and login system
- **Task Management**: Create, update, and delete tasks
- **List Organization**: Group tasks into custom lists
- **Category System**: Categorize tasks (Personal, University, etc.)
- **Email Integration**: Email notifications via Nodemailer
- **Responsive UI**: Modern, Bootstrap-based interface
- **Profile Management**: User profile customization

## 🛠 Tech Stack

### Frontend
- **React** 18.2.0 - UI framework
- **TypeScript** - Type-safe development
- **React Bootstrap** - UI components
- **Axios** - HTTP client
- **MDB React UI Kit** - Additional UI components

### Backend
- **Node.js** with **Express** - Server framework
- **TypeScript** - Type-safe development
- **SQLite3** - Database
- **Nodemailer** - Email service
- **Nodemon** - Development hot-reload

## 📁 Project Structure

```
UAlly/
├── backend/                # Backend server
│   ├── src/
│   │   ├── main.ts        # Main server file with API endpoints
│   │   ├── serverInfo.ts  # Server configuration
│   │   └── tables/        # Database models
│   │       ├── Users.ts   # User model
│   │       ├── Tasks.ts   # Task model
│   │       ├── Lists.ts   # List model
│   │       └── Categories.ts # Category model
│   ├── db/                # SQLite database
│   └── build/             # Compiled JavaScript
│
├── frontend/              # React frontend
│   ├── src/
│   │   ├── App.tsx        # Main app component
│   │   ├── components/    # React components
│   │   │   ├── BaseLayout.tsx
│   │   │   ├── Header.tsx
│   │   │   ├── SideBar.tsx
│   │   │   ├── Task.tsx
│   │   │   └── ...
│   │   ├── views/         # Page views
│   │   │   ├── LoginView.tsx
│   │   │   ├── RegisterView.tsx
│   │   │   ├── ProjectView.tsx
│   │   │   └── ...
│   │   └── assets/        # Images and styles
│   └── build/             # Production build
│
└── README.md              # This file
```

## 🚀 Getting Started

### Prerequisites

- Node.js (v16 or higher)
- npm or yarn
- SQLite3

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd UAlly
   ```

2. **Install Backend Dependencies**
   ```bash
   cd backend
   npm install
   ```

3. **Install Frontend Dependencies**
   ```bash
   cd ../frontend
   npm install
   ```

4. **Configure Server Settings**
   
   Create a `serverInfo.json` file in `backend/server/`:
   ```json
   {
     "smtp": {
       "host": "your-smtp-host",
       "port": 587,
       "auth": {
         "user": "your-email@example.com",
         "pass": "your-password"
       }
     }
   }
   ```

5. **Initialize Database**
   
   The database will be automatically initialized with the SQL schemas in `backend/src/tables/` when you first run the backend.

## 🏃 Running the Application

### Development Mode

1. **Start the Backend Server**
   ```bash
   cd backend
   npm run dev
   ```
   The server will run with hot-reload enabled and will restart on any TypeScript file changes.

2. **Start the Frontend Development Server**
   ```bash
   cd frontend
   npm start
   ```
   The application will open in your browser at `http://localhost:3000`

### Production Mode

1. **Build the Backend**
   ```bash
   cd backend
   npm run compile
   ```

2. **Build the Frontend**
   ```bash
   cd frontend
   npm run build
   ```
   The production build will be created in the `frontend/build/` directory.

## 🔌 API Endpoints

The backend provides RESTful API endpoints for:

### User Management
- `POST /registerUser` - Register a new user
- `POST /loginUser` - User login
- `GET /getUser/:email` - Get user details
- `DELETE /deleteUser/:email` - Delete user account
- `POST /updateUser` - Update user information

### Task Management
- `POST /addTask` - Create a new task
- `GET /getTasks/:userEmail` - Get all tasks for a user
- `DELETE /deleteTask/:taskId` - Delete a task
- `POST /updateTask` - Update task details

### List Management
- `POST /addList` - Create a new list
- `GET /getLists/:userEmail` - Get all lists for a user
- `DELETE /deleteList/:listId` - Delete a list
- `POST /updateList` - Update list details

### Category Management
- `POST /addCategory` - Create a new category
- `GET /getCategories/:userEmail` - Get all categories for a user
- `DELETE /deleteCategory/:categoryId` - Delete a category
- `POST /updateCategory` - Update category details

## 👥 Authors

- Helena
- Rui
- Vasco

## 📄 License

ISC

## 🤝 Contributing

This is an academic project. For any questions or suggestions, please contact the authors.

---

**Note**: Make sure to configure your SMTP settings in `backend/server/serverInfo.json` before running the application to enable email functionality.
