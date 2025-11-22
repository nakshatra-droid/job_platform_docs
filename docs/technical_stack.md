# Technical Stack

This section describes the **technical foundation** of the **Joblelo Platform** project — covering all technologies, tools, and services used across the frontend, backend, and deployment layers.  

The stack has been carefully selected to ensure **scalability**, **security**, **maintainability**, and **performance** for a real-world, production-ready system.

---

## Frontend

| Component | Technology | Purpose |
|------------|-------------|----------|
| **Framework** | React.js | Builds a dynamic, single-page application with component-based UI. |
| **Styling** | Tailwind CSS | Provides responsive, utility-first CSS design for consistency and speed. |
| **Hosting Platform** | Vercel | Deployed for fast, global delivery with automatic builds. |
| **Routing & State** | React Router | Handles navigation and user authentication states. |
| **API Communication** | Axios | Sends HTTP requests securely to backend endpoints. |
| **PWA Support (Optional)** | Service Worker | Enables offline capability and “Add to Home Screen” option. |

---

## Backend

| Component | Technology | Purpose |
|------------|-------------|----------|
| **Runtime Environment** | Node.js | Executes JavaScript code on the server side. |
| **Framework** | Express.js | Provides REST API structure, middleware support, and routing. |
| **Authentication** | JWT (JSON Web Token) | Manages secure login and role-based access control. |
| **File Handling** | Multer | Handles multipart/form-data for file. |
| **Hosting** | AWS EC2 | Runs backend application in a scalable cloud environment. |

---

## Database Layer

| Component | Technology | Purpose |
|------------|-------------|----------|
| **Database** | PostgreSQL | Relational database used for structured data such as users, jobs, and applications. |
| **Hosting Service** | AWS RDS (Relational Database Service) | Manages PostgreSQL instance with high availability, backups, and monitoring. |

---

## Cloud Services (AWS)

| Service | Purpose |
|----------|----------|
| **Amazon EC2** | Hosts the Node.js backend server in a managed Linux environment. |
| **Amazon RDS (PostgreSQL)** | Stores relational data with reliability, scaling, and monitoring. |

---

## Authentication & Authorization

| Aspect | Description |
|--------|--------------|
| **Authentication Type** | JWT-based authentication using access and refresh tokens. |
| **User Roles** | `Job Seeker`, `Employer`|
| **Token Flow** | Tokens are generated at login and verified for protected routes. |
| **Security Practices** | Passwords hashed using bcrypt. |
| **Access Control** | Role-based middleware ensures proper permission boundaries. |

---

## Development Tools

| Tool | Purpose |
|------|----------|
| **Git & GitHub** | Version control and collaboration. |
| **Postman** | API testing and endpoint validation. |
| **VS Code** | Development environment with extensions for linting and formatting. |
| **Nodemon** | Auto-restarts backend during development. |

---

## Deployment & CI/CD

| Component | Technology | Purpose |
|------------|-------------|----------|
| **Frontend Deployment** | Vercel | Continuous deployment from main branch with build triggers. |
| **Backend Deployment** | AWS EC2 | Deployed Node.js server configured with PM2 for process management. |
| **Database** | AWS RDS (PostgreSQL) | Managed cloud database service. |
| **CI/CD Pipeline** | GitHub Actions | Automates testing, build, and deployment on every push. |
