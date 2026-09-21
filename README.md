# Advanced Web Development Framework (AWDF) - Practicals Portfolio

Welcome to the **AWDF Practicals Portfolio** repository! This repository contains a collection of practical exercises and full-stack web applications developed as part of the Advanced Web Development Framework curriculum.

---

## 📂 Repository Structure

| Folder | Title & Description | Tech Stack |
| :--- | :--- | :--- |
| [`pra-1`](./pra-1) | **React Basics & Component Architecture** <br> Introduction to React components, props, and Vite build tooling. | React, Vite |
| [`pra-2`](./pra-2) | **React State & Event Handling** <br> Interactive state management, form controls, and dynamic UI updates. | React, Vite |
| [`pra-3`](./pra-3) | **React Hooks & Component Lifecycle** <br> Usage of `useState`, `useEffect`, and component modularity. | React, Vite |
| [`pra-4`](./pra-4) | **Node.js & Express API Server** <br> Building a basic Node.js Express server with RESTful endpoints. | Node.js, Express |
| [`pra-5`](./pra-5) | **Express Middleware & MongoDB Integration** <br> Integrating MongoDB with Mongoose, custom logger, and validation middleware. | Express, Mongoose, MongoDB |
| [`pra-6`](./pra-6) | **Full Stack Task Manager (MERN)** <br> Complete full-stack Task Manager connecting React frontend to Express + MongoDB backend. | React, Vite, Express, MongoDB |
| [`pra-7`](./pra-7) | **JWT Authentication & Server-Side Validation API** <br> REST API with User Authentication (`bcrypt` password hashing, JWT tokens) and protected task routes. | Node.js, Express, JWT, bcryptjs, Mongoose |
| [`pra-8`](./pra-8) | **React Performance Optimization & Lazy Loading** <br> Full-stack app optimized using route-based code splitting with `React.lazy()` and `Suspense`. | React, Vite, React Router, Express, MongoDB |

---

## 🛠️ Technology Stack

- **Frontend**: React 19, Vite, React Router DOM, HTML5, CSS3
- **Backend**: Node.js, Express 5
- **Database**: MongoDB & Mongoose ORM
- **Security & Authentication**: JSON Web Tokens (`jsonwebtoken`), Password Hashing (`bcryptjs`)
- **Optimization**: Code splitting (`React.lazy`), Suspense loading, Vite bundling

---

## 🚀 Getting Started

Each practical folder is self-contained. To run any individual practical:

1. Navigate to the target practical directory:
   ```bash
   cd pra-X   # Replace X with the practical number (e.g., pra-6, pra-7, pra-8)
   ```

2. For Single Projects (Backend or Frontend):
   ```bash
   npm install
   npm run dev   # or npm start
   ```

3. For Full-Stack Projects (`pra-6`, `pra-8`):
   - **Backend**:
     ```bash
     cd backend
     npm install
     npm run dev
     ```
   - **Frontend**:
     ```bash
     cd frontend
     npm install
     npm run dev
     ```

---

## 📝 License

This repository is maintained for academic practical submissions.
