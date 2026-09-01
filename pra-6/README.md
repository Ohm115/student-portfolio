# Practical 6 - Full Stack Task Manager (MERN Stack)

This repository contains Practical 6: a full-stack Task Manager application built using **React + Vite** for the frontend, **Node.js + Express** for the backend REST API, and **MongoDB (Mongoose)** for data storage.

---

## 📁 Project Structure

```text
pra-6/
├── backend/            # Express REST API Server
│   ├── models/         # Mongoose Data Models (Task.js)
│   ├── .env.example    # Sample environment configuration
│   ├── package.json    # Backend dependencies & scripts
│   └── server.js       # Entry point for backend server
└── frontend/           # React single-page application (Vite)
    ├── public/         # Static assets
    ├── src/            # Components, API calls, and styles
    ├── .env.example    # Sample frontend environment config
    └── package.json    # Frontend dependencies & scripts
```

---

## 🚀 Quick Start Guide

### 1. Backend Setup

```bash
cd backend
npm install
npm run dev
```

The backend server will start on `http://localhost:5000`.

> **Environment Variables**: Make a copy of `.env.example` named `.env` in `backend/` if you want to override default ports or MongoDB URI:
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

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/tasks` | Fetch all tasks |
| `POST` | `/tasks` | Create a new task (`{ title, description, completed }`) |
| `PUT` | `/tasks/:id` | Update an existing task by ID |
| `DELETE` | `/tasks/:id` | Delete a task by ID |

---

## 🛠️ Tech Stack

- **Frontend**: React 19, Vite, Vanilla CSS
- **Backend**: Node.js, Express 5, Mongoose
- **Database**: MongoDB
