# Practical 10 - Asynchronous Event-Driven Architecture with Node.js EventEmitter (Full-Stack MERN)

This repository contains Practical 10: a full-stack Task Manager application demonstrating **Asynchronous Event-Driven Architecture** using Node.js's built-in `EventEmitter` and `setImmediate()` in an Express + MongoDB backend, integrated with in-memory caching (`node-cache`) and a **React + Vite** frontend.

---

## 📁 Project Structure

```text
pra-10/
├── backend/            # Express REST API Server with EventEmitter & In-Memory Caching
│   ├── models/         # Mongoose Data Models (Task.js with assignedUser support)
│   ├── .env.example    # Sample environment configuration
│   ├── package.json    # Backend dependencies (express, mongoose, node-cache, cors, dotenv)
│   └── server.js       # Express server with EventEmitter event listeners & async triggers
├── frontend/           # React single-page application (Vite)
│   ├── public/         # Static assets & icons
│   ├── src/            # Components, API client, pages, and styles
│   │   ├── pages/      # Home, Projects (Task Manager), Contact
│   │   ├── api.js      # Fetch API integration
│   │   ├── App.css     # Responsive modern styling
│   │   ├── App.jsx     # App router with React.lazy & Suspense
│   │   └── main.jsx    # Application entry point
│   └── package.json    # Frontend dependencies & scripts
├── .gitignore          # Ignored files (node_modules, .env, dist)
└── README.md           # Practical documentation
```

---

## ⚡ Key Features & Concepts

### 1. Asynchronous Event-Driven Architecture (`EventEmitter`)
- **Node.js `events` Module**: Built-in pub/sub architecture using a shared `taskEvents` instance (`new EventEmitter()`).
- **Decoupled Event Listeners**:
  - Listens on `"task-created"` events independently from the HTTP request/response cycle.
  - Simulates non-blocking asynchronous email/SMS notification workers (`setTimeout` delay without holding the HTTP response).
- **Non-Blocking Dispatch via `setImmediate()`**:
  - The API responds immediately to the client with `201 Created` (`{ message: "Task created successfully", task: savedTask }`).
  - Event emission is deferred to the next iteration of the Node.js event loop using `setImmediate()`, ensuring maximum API throughput and low latency.
- **Console Audit Logs**:
  ```text
  API response sent at: 2026-10-18T14:00:45.123Z

  ===== TASK NOTIFICATION =====
  Task Title: Implement Authentication
  Assigned User: Ohm
  Timestamp: 2026-10-18T14:00:46.125Z
  =============================
  ```

### 2. In-Memory Server Caching (`node-cache`)
- **Fast Response Retrieval**: 60-second TTL caching on `GET /tasks` (`X-Cache: HIT` / `X-Cache: MISS`).
- **Automatic Cache Invalidation**: `POST`, `PUT`, and `DELETE` requests automatically invalidate cached task lists (`allTasks`).
- **Diagnostics**: `GET /debug/cache` provides hit/miss statistics and active cache key metrics.

### 3. Full-Stack React Frontend
- **React 19 + Vite**: Modern, responsive UI with Vite build tooling and React Router DOM.
- **Route-Level Code Splitting**: Utilizes `React.lazy()` and `Suspense` fallback loaders.
- **Task Assignment Support**: Intuitive task creation form with task title, description, and assigned user.

---

## 🚀 Quick Start Guide

### 1. Backend Setup

```bash
cd backend
npm install
npm run dev   # or npm start
```

The backend server starts on `http://localhost:5000`.

> **Environment Variables**: Create a `.env` file inside `backend/` (or copy `.env.example`):
> ```env
> PORT=5000
> MONGO_URI=mongodb://localhost:27017/taskmanager
> ```

---

### 2. Frontend Setup

```bash
cd frontend
npm install
npm run dev
```

Open your browser at `http://localhost:5173`.

---

## 🔌 API Endpoints

| Method | Endpoint | Cache / Event Behavior | Description |
| :--- | :--- | :--- | :--- |
| `GET` | `/tasks` | Cached (`allTasks`, 60s TTL) | Fetch all tasks (Returns `X-Cache: HIT` or `MISS`) |
| `GET` | `/tasks/:id` | Cached (`task_:id`, 60s TTL) | Fetch single task by ID |
| `POST` | `/tasks` | Emits `task-created` + Clears `allTasks` cache | Create a task, respond immediately, and trigger background notification |
| `PUT` | `/tasks/:id` | Cache Invalidation (`allTasks`, `task_:id`) | Update an existing task |
| `DELETE` | `/tasks/:id` | Cache Invalidation (`allTasks`, `task_:id`) | Delete a task |
| `GET` | `/debug/cache` | Dynamic / Non-cached | Retrieve cache hit/miss statistics & active keys |

---

## 🛠️ Tech Stack

- **Frontend**: React 19, Vite, React Router DOM, Vanilla CSS
- **Backend**: Node.js, Express 5, `EventEmitter` (`events`), `node-cache`, Mongoose
- **Database**: MongoDB
