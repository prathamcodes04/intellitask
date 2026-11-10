# TaskFlow AI – Intelligent Task Management System

A full-stack task management application that combines a clean task management interface with AI-powered natural language commands. Create, update, delete, and track tasks using either the UI or simple everyday language.

## ✨ Features

- **Task Management:** Create, view, update, and delete tasks.
- **AI-Powered Commands:** Manage tasks using natural language.
- **Task Status Tracking:** Track tasks through three stages:
  - Not Started
  - In Progress
  - Completed
- **Smart Task Filtering:** Filter tasks based on their current status.
- **AI Intent Interpretation:** Converts user commands into structured JSON actions.
- **Centralized Business Logic:** Both UI and AI interactions use the same backend services.
- **MongoDB Integration:** Persist task data using MongoDB Atlas or a local MongoDB instance.
- **REST API:** Backend endpoints for task operations.

## 🛠️ Tech Stack

| Layer | Technologies |
|---|---|
| Frontend | React, Vite, CSS |
| Backend | Node.js, Express.js |
| Database | MongoDB, Mongoose |
| AI Integration | Groq API |
| AI Model | openai/gpt-oss-20b |
| API Testing | Postman |
| Version Control | Git, GitHub |

## 🏗️ Architecture

```text
             USER
               |
       +-------+-------+
       |               |
    UI MODE          AI MODE
       |               |
       |         Natural Language
       |               |
       |          Groq API
       |               |
       +-------+-------+
               |
          REST API
               |
        Node.js / Express
               |
        SERVICE LAYER
          /       \
   Task Service  AI Service
          \       /
           MongoDB
```

The application separates AI interpretation from business logic. The AI identifies the user's intended action, while the backend validates and executes the operation.

## 📁 Project Structure

```text
taskflow-ai/
│
├── backend/
│   ├── config/
│   │   └── db.js
│   │
│   ├── middleware/
│   │   ├── asyncHandler.js
│   │   └── errorHandler.js
│   │
│   ├── models/
│   │   └── taskModel.js
│   │
│   ├── routes/
│   │   ├── taskRoutes.js
│   │   └── aiRoutes.js
│   │
│   ├── services/
│   │   ├── taskService.js
│   │   └── aiService.js
│   │
│   ├── .env
│   ├── server.js
│   └── package.json
│
├── frontend/
│   ├── src/
│   │   ├── App.jsx
│   │   ├── App.css
│   │   ├── main.jsx
│   │   └── index.css
│   │
│   ├── index.html
│   └── package.json
│
├── .gitignore
└── README.md
```

## 🚀 Getting Started

### Prerequisites

- Node.js (v18 or higher)
- npm
- MongoDB Atlas account or local MongoDB
- Groq API key

### 1. Clone the Repository

```bash
git clone https://github.com/prathamcodes04/task-manager.git
cd task-manager
```

### 2. Backend Setup

```bash
cd backend
npm install
```

Create a `.env` file inside the backend directory:

```env
PORT=5000
NODE_ENV=development
MONGODB_URI=your_mongodb_connection_string
GROQ_API_KEY=your_groq_api_key
```

Start the backend:

```bash
npm run dev
```

The backend server will run at:

`http://localhost:5000`

### 3. Frontend Setup

Open another terminal:

```bash
cd frontend
npm install
npm run dev
```

Open the frontend URL shown in your terminal, usually:

`http://localhost:5173`

## 🤖 AI-Powered Task Management

The application uses the Groq API to interpret natural language commands.

The AI acts as an intent interpreter and converts user instructions into structured JSON. The backend then validates and executes the corresponding operation.

### Example Commands

| User Command | Expected Action |
|---|---|
| Create a task called Buy groceries | Create task |
| Start Buy groceries | Update status to In Progress |
| Mark Buy groceries as done | Update status to Completed |
| Show all completed tasks | List completed tasks |
| Delete Buy groceries | Delete task |

### Example AI Intent

```json
{
  "action": "update_state",
  "taskName": "Buy groceries",
  "targetState": "Completed",
  "filterState": null,
  "confidence": "high",
  "ambiguity": null
}
```

## 📡 API Documentation

Base URL:

```text
http://localhost:5000/api
```

| Method | Endpoint | Description |
|---|---|---|
| POST | `/tasks` | Create a task |
| GET | `/tasks` | Retrieve all tasks |
| GET | `/tasks/:id` | Retrieve a specific task |
| PATCH | `/tasks/:id/state` | Update task status |
| DELETE | `/tasks/:id` | Delete a task |
| POST | `/ai/command` | Execute a natural-language command |

### Example: Create a Task

**Request**

```http
POST /api/tasks
Content-Type: application/json
```

```json
{
  "name": "Complete assignment"
}
```

**Expected Response – 201 Created**

```json
{
  "success": true,
  "data": {
    "_id": "your_generated_task_id",
    "name": "Complete assignment",
    "state": "Not Started"
  },
  "message": "Task created successfully"
}
```

*Note: Response fields may include additional timestamps and other model properties.*

### Example: AI Command

**Request**

```http
POST /api/ai/command
Content-Type: application/json
```

```json
{
  "command": "Mark Complete assignment as done"
}
```

## 🔐 Environment Variables

| Variable | Description |
|---|---|
| PORT | Backend server port |
| NODE_ENV | Application environment |
| MONGODB_URI | MongoDB connection string |
| GROQ_API_KEY | Groq API authentication key |

**Security:** Never commit your `.env` file or expose your API keys publicly. Add `.env` to `.gitignore`.

## 🧠 Key Design Decisions

1. **Separation of Concerns:** Routes, services, and database models have separate responsibilities.
2. **AI as an Intent Interpreter:** AI interprets commands but does not directly access or modify the database.
3. **Centralized Validation:** Task operations and state transitions are handled by backend services.
4. **Persistent Storage:** MongoDB stores task records.
5. **RESTful Design:** Frontend and backend communicate through REST API endpoints.

## 🔮 Future Improvements

- User authentication and authorization.
- Task deadlines and priority levels.
- Search and advanced filtering.
- Task reminders and notifications.
- Dashboard with task analytics.
- Improved AI command handling.

## 👨‍💻 Author

**Pratham Gupta**

GitHub: [@prathamcodes04](https://github.com/prathamcodes04)

---

⭐ If you find this project useful, consider giving it a star!
