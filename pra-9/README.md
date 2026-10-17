# Practical 9 - Backend In-Memory Caching with NodeCache (Full-Stack MERN)

This repository contains Practical 9: a full-stack Task Manager application demonstrating **Server-Side In-Memory Caching** using `node-cache` in an Express + MongoDB backend, paired with an optimized **React + Vite** frontend.

---

## 📁 Project Structure

```text
pra-9/
├── backend/            # Express REST API Server with In-Memory Caching
│   ├── models/         # Mongoose Data Models (Task.js)
│   ├── .env.example    # Sample environment configuration
│   ├── package.json    # Backend dependencies (express, mongoose, node-cache, cors, dotenv)
│   └── server.js       # Express server with cache logic & debug endpoints
├── frontend/           # React single-page application (Vite)
│   ├── public/         # Static assets
│   ├── src/            # Components, API client, pages, and styles
│   │   ├── pages/      # Home, Projects (Task Manager), Contact
│   │   ├── api.js      # Fetch API integration
│   │   ├── App.jsx     # App router with React.lazy & Suspense
│   │   └── main.jsx    # Application entry point
│   └── package.json    # Frontend dependencies & scripts
└── README.md           # Practical documentation
```

---

## ⚡ Key Features & Concepts

### 1. In-Memory Server Caching (`node-cache`)
- **Configured TTL**: Default Time-To-Live (TTL) of 60 seconds (`stdTTL: 60`, `checkperiod: 120`).
- **Cache Headers**: Custom `X-Cache: HIT` or `X-Cache: MISS` HTTP response headers allow clients to verify cache status.
- **Cache Invalidation**:
  - `POST /tasks` invalidates the cached task collection (`allTasks`).
  - `PUT /tasks/:id` and `DELETE /tasks/:id` invalidate both `allTasks` and the individual task item `task_:id`.
- **Cache Analytics & Diagnostics**: `GET /debug/cache` provides real-time statistics:
  - Cache Hits & Misses count
  - Total requests processed
  - Cache Hit Rate percentage (`hitRate`)
  - Currently active cache keys (`cachedKeys`)

### 2. Frontend Application
- **Lazy Loading**: Route-level code splitting using `React.lazy()` and `Suspense` for optimal bundle size and loading speed.
- **Task Management UI**: Interactive interface to create, list, toggle completion status, and delete tasks.

---

## 🚀 Quick Start Guide

### 1. Backend Setup

```bash
cd backend
npm install
npm run dev
```

The backend server starts on `http://localhost:5000`.

> **Environment Variables**: Create a `.env` file inside `backend/` (or copy `.env.example`):
> ```env
> PORT=5000
> MONGO_URI=mongodb://127.0.0.1:27017/taskmanager
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

| Method | Endpoint | Cache Behavior | Description |
| :--- | :--- | :--- | :--- |
| `GET` | `/tasks` | Cached (`allTasks`, 60s TTL) | Fetch all tasks (Returns `X-Cache: HIT` or `MISS`) |
| `GET` | `/tasks/:id` | Cached (`task_:id`, 60s TTL) | Fetch single task by ID |
| `POST` | `/tasks` | Cache Invalidation (`allTasks`) | Create a new task |
| `PUT` | `/tasks/:id` | Cache Invalidation (`allTasks`, `task_:id`) | Update an existing task |
| `DELETE` | `/tasks/:id` | Cache Invalidation (`allTasks`, `task_:id`) | Delete a task |
| `GET` | `/debug/cache` | Dynamic / Non-cached | Retrieve cache hit/miss statistics & active keys |

---

## 🛠️ Tech Stack

- **Frontend**: React 19, Vite, React Router DOM, Vanilla CSS
- **Backend**: Node.js, Express 5, `node-cache`, Mongoose
- **Database**: MongoDB
