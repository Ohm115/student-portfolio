# Practical 11 - Docker Containerization & Multi-Container Orchestration with Docker Compose (Full-Stack MERN)

This repository contains Practical 11: a complete, production-ready **Docker Containerization and Multi-Container Orchestration** setup for the full-stack MERN Task Manager application using **Docker**, **Multi-Stage Builds**, and **Docker Compose**.

---

## 📁 Project Structure

```text
pra-11/
├── backend/                  # Express REST API Server
│   ├── models/               # Mongoose Data Models (Task.js)
│   ├── .dockerignore         # Excludes node_modules, .env, and logs from Docker context
│   ├── .env.example          # Sample environment variables
│   ├── Dockerfile            # Lightweight Node.js 20 Alpine container image
│   ├── package.json          # Backend dependencies
│   └── server.js             # Express server with EventEmitter & in-memory caching
├── frontend/                 # React Single Page Application (Vite)
│   ├── public/               # Static assets & icons
│   ├── src/                  # React components, pages, and styles
│   ├── .dockerignore         # Excludes node_modules, dist, and logs from Docker context
│   ├── Dockerfile            # Multi-stage build (Node 20 build -> Nginx Alpine runtime)
│   ├── package.json          # Frontend dependencies
│   └── vite.config.js        # Vite configuration
├── .gitignore                # Git ignore rules
├── docker-compose.yml        # Multi-container orchestration (Frontend, Backend, MongoDB)
└── README.md                 # Practical documentation
```

---

## ⚡ Key Features & Concepts

### 1. Multi-Stage Dockerfile for React Frontend
- **Stage 1 (Build)**: Uses `node:20-alpine` to install dependencies and compile the production bundle (`npm run build`).
- **Stage 2 (Production Server)**: Uses ultra-lightweight `nginx:alpine` to serve static assets from `/usr/share/nginx/html`.
- **Port Exposure**: Listens on port `80` inside the container, mapped to `5173` on the host.

### 2. Optimized Backend Dockerfile
- **Base Image**: `node:20-alpine` for minimal footprint and enhanced security.
- **Dependency Optimization**: Runs `npm install --omit=dev` to install only production dependencies.
- **Port Exposure**: Listens on port `5000` inside the container, mapped to `5000` on the host.

### 3. Docker Compose Orchestration (`docker-compose.yml`)
- **Three Coordinated Services**:
  1. `frontend` (`task-frontend`): React + Nginx frontend mapped to host port `5173`.
  2. `backend` (`task-backend`): Express REST API connected to MongoDB via container DNS (`mongodb://mongodb:27017/taskdb`).
  3. `mongodb` (`task-mongodb`): Official `mongo:7` image with container health checks and persistent volume storage.
- **Container Health Check**:
  ```yaml
  healthcheck:
    test: ["CMD", "mongosh", "--quiet", "--eval", "db.adminCommand('ping').ok"]
    interval: 5s
    timeout: 3s
    retries: 10
  ```
  The backend container waits for MongoDB to be completely healthy before starting (`condition: service_healthy`).
- **Data Persistence**: Uses a named volume (`mongodb-data`) to persist MongoDB data across container restarts.
- **Isolated Bridge Network**: All services communicate securely within the custom `app-network` bridge.

---

## 🚀 Running with Docker Compose

Ensure [Docker](https://www.docker.com/) and [Docker Compose](https://docs.docker.com/compose/) are installed and running.

### 1. Build and Start All Containers

From the `pra-11` root directory:

```bash
docker compose up --build
```

To run in detached background mode:

```bash
docker compose up -d --build
```

### 2. Access the Applications

- **Frontend (Web UI)**: [http://localhost:5173](http://localhost:5173)
- **Backend API**: [http://localhost:5000](http://localhost:5000)
- **MongoDB**: `localhost:27017`

### 3. Check Container Status & Logs

```bash
# View running containers
docker compose ps

# View real-time logs
docker compose logs -f

# View backend logs specifically
docker compose logs -f backend
```

### 4. Stop and Clean Up Containers

```bash
# Stop containers
docker compose down

# Stop containers and remove volumes (clean database reset)
docker compose down -v
```

---

## 💻 Running Locally Without Docker

### 1. Backend Setup
```bash
cd backend
npm install
npm run dev   # or npm start
```

### 2. Frontend Setup
```bash
cd frontend
npm install
npm run dev
```

---

## 🔌 API Endpoints

| Method | Endpoint | Cache / Event Behavior | Description |
| :--- | :--- | :--- | :--- |
| `GET` | `/tasks` | Cached (`allTasks`, 60s TTL) | Fetch all tasks (Returns `X-Cache: HIT` or `MISS`) |
| `GET` | `/tasks/:id` | Cached (`task_:id`, 60s TTL) | Fetch single task by ID |
| `POST` | `/tasks` | Emits `task-created` + Invalidation | Create a task and trigger asynchronous notification |
| `PUT` | `/tasks/:id` | Invalidation (`allTasks`, `task_:id`) | Update an existing task |
| `DELETE` | `/tasks/:id` | Invalidation (`allTasks`, `task_:id`) | Delete a task |
| `GET` | `/debug/cache` | Dynamic / Non-cached | Retrieve cache hit/miss statistics & active keys |

---

## 🛠️ Tech Stack

- **Containerization & Orchestration**: Docker, Docker Compose, Nginx Alpine, Multi-Stage Builds
- **Frontend**: React 19, Vite, React Router DOM, Vanilla CSS
- **Backend**: Node.js, Express 5, `EventEmitter`, `node-cache`, Mongoose
- **Database**: MongoDB 7 (`mongo:7` image)
