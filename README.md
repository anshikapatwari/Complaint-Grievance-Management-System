

<h1 align="center">🛡️ NMIMS Grievance Management System</h1>

<p align="center">
  <strong>A role-based, SLA-driven grievance tracking portal built for SVKM's NMIMS </strong>
  <br/>
  <em>Agile & Prod. Development — Full-Stack PERN Application with DevOps Integration</em>
</p>

<p align="center">
  <a href="#-features">Features</a> •
  <a href="#%EF%B8%8F-tech-stack">Tech Stack</a> •
  <a href="#-architecture">Architecture</a> •
  <a href="#-getting-started">Getting Started</a> •
  <a href="#-api-reference">API Reference</a> •
  <a href="#-devops-pipeline">DevOps</a> •
  <a href="#-project-structure">Structure</a>
</p>

---

## 🌟 Features

### 🔐 Authentication & Authorization
- **JWT-based authentication** with secure token management
- **Role-Based Access Control (RBAC)** — `USER`, `AUTHORITY`, and `ADMIN` roles
- **Bcrypt password hashing** for secure credential storage
- **Pre-seeded admin account** for instant authority access

### 📋 Grievance Lifecycle Management
- **Submit grievances** with category tagging and optional anonymous reporting
- **SLA Engine** — Automatic resolution deadline calculation based on priority level
- **Priority management** — `LOW` → 14 days | `MEDIUM` → 7 days | `HIGH` → 2 days | `CRITICAL` → 24 hours
- **Status tracking** — `SUBMITTED` → `IN_PROGRESS` → `RESOLVED` → `CLOSED`
- **Priority & SLA fields are admin-only** — Students are shielded from administrative complexity

### 💬 Real-Time Communication
- **Threaded comment system** on each grievance for student–authority dialogue
- **Timeline-based discussion view** with role-tagged messages

### 📊 Admin Command Center
- **Analytics dashboard** with stat cards (Total Cases, Action Required, Resolved, Critical SLA)
- **Inline status and priority controls** — Admins can update directly from the table view
- **Audit logging** — Every status change, priority update, and comment is permanently recorded

### 🎨 Premium UI/UX
- **NMIMS-branded glassmorphic design** with custom color palette
- **Responsive layouts** optimized for desktop and mobile
- **Micro-animations** and hover effects for a polished experience
- **Anonymous submission masking** — Names hidden from non-admin viewers

---

## 🛠️ Tech Stack

### Backend
| Technology | Purpose |
|:---|:---|
| **Node.js** | Server-side JavaScript runtime |
| **Express 5** | Web framework for RESTful API routing and middleware |
| **Prisma ORM** | Type-safe database client with migrations and schema management |
| **PostgreSQL 15** | Relational database for persistent storage |
| **JWT** | Stateless authentication via JSON Web Tokens |
| **Bcryptjs** | Password hashing with salt rounds |

### Frontend
| Technology | Purpose |
|:---|:---|
| **React 18** | Component-based UI library with hooks |
| **Vite** | Lightning-fast HMR dev server and build tool |
| **Tailwind CSS v4** | Utility-first CSS framework for NMIMS-branded styling |
| **Axios** | Promise-based HTTP client for API communication |
| **Lucide React** | Modern, consistent icon library |
| **React Router v7** | Client-side routing with protected routes |

### DevOps & Infrastructure
| Technology | Purpose |
|:---|:---|
| **Docker** | Containerized PostgreSQL database |
| **Docker Compose** | Multi-service orchestration |
| **Jenkins** | CI/CD pipeline automation |
| **Kubernetes** | Container orchestration with replicated deployments |
| **Git** | Version control |

---

## 🏗 Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                        CLIENT (Browser)                     │
│                  React 18 + Vite + Tailwind                 │
│              ┌──────────────────────────────┐               │
│              │  AuthContext (JWT in State)   │               │
│              └──────────┬───────────────────┘               │
│                         │ Axios (HTTP)                      │
└─────────────────────────┼───────────────────────────────────┘
                          │ :5173 → :5000
┌─────────────────────────┼───────────────────────────────────┐
│                   BACKEND (Express 5)                       │
│              ┌──────────┴───────────────────┐               │
│              │     REST API (JSON)          │               │
│              │  /api/auth    → JWT Auth     │               │
│              │  /api/complaints → CRUD + SLA│               │
│              └──────────┬───────────────────┘               │
│              ┌──────────┴───────────────────┐               │
│              │  Middleware: CORS, Auth, RBAC │               │
│              └──────────┬───────────────────┘               │
│              ┌──────────┴───────────────────┐               │
│              │     Prisma ORM Client        │               │
│              └──────────┬───────────────────┘               │
└─────────────────────────┼───────────────────────────────────┘
                          │ :5433
┌─────────────────────────┼───────────────────────────────────┐
│              PostgreSQL 15 (Docker Container)               │
│              ┌──────────┴───────────────────┐               │
│              │  Tables:                     │               │
│              │  • User (RBAC roles)         │               │
│              │  • Complaint (SLA + status)  │               │
│              │  • Comment (threaded chat)   │               │
│              │  • AuditLog (full trail)     │               │
│              └──────────────────────────────┘               │
└─────────────────────────────────────────────────────────────┘
```

---

## 🚀 Getting Started

### Prerequisites

Ensure the following are installed on your system:

| Tool | Download |
|:---|:---|
| **Node.js** (v18+) | [nodejs.org](https://nodejs.org/) |
| **Docker Desktop** | [docker.com](https://www.docker.com/products/docker-desktop/) |
| **Git** | [git-scm.com](https://git-scm.com/) |

### 1. Clone the Repository

```bash
git clone https://github.com/<your-username>/nmims-grievance-portal.git
cd nmims-grievance-portal
```

### 2. Start the PostgreSQL Database

Make sure Docker Desktop is running, then:

```bash
docker-compose up db -d
```

> This starts a PostgreSQL 15 container on port **5433** with pre-configured credentials.

### 3. Setup the Backend

```bash
cd backend
npm install
```

The `.env` file is pre-configured with:

```env
DATABASE_URL="postgresql://nmims_admin:nmims_password@localhost:5433/nmims_grievance_db?schema=public"
JWT_SECRET="nmims_super_secret_key"
PORT=5000
```

Run the database migration and seed the admin account:

```bash
npx prisma migrate dev --name init
npx prisma db seed
```

Start the backend server:

```bash
npm start
```

> ✅ You should see: `Server running on port 5000`

### 4. Setup the Frontend

Open a **second terminal**:

```bash
cd frontend
npm install
npm run dev
```

> ✅ The app will be available at `http://localhost:5173`

### 5. Login

| Role | Email | Password |
|:---|:---|:---|
| **Admin** | `admin@nmims.edu` | `nmims_admin_2026` |
| **Student** | Register via the Sign Up page | — |

---

## 📡 API Reference

All endpoints are prefixed with `http://localhost:5000/api`

### Authentication

| Method | Endpoint | Description | Auth |
|:---|:---|:---|:---|
| `POST` | `/auth/register` | Register a new student account | ❌ |
| `POST` | `/auth/login` | Login and receive JWT token | ❌ |

**Register Request Body:**
```json
{
  "name": "John Doe",
  "email": "john@nmims.edu",
  "password": "securepassword"
}
```

**Login Response:**
```json
{
  "token": "eyJhbGciOiJIUzI1...",
  "user": { "id": "uuid", "name": "John Doe", "role": "USER" }
}
```

### Grievances

| Method | Endpoint | Description | Auth | Roles |
|:---|:---|:---|:---|:---|
| `POST` | `/complaints` | Submit a new grievance | ✅ | All |
| `GET` | `/complaints` | List grievances (role-filtered) | ✅ | All |
| `PUT` | `/complaints/:id/status` | Update status/priority | ✅ | `ADMIN`, `AUTHORITY` |

### Comments

| Method | Endpoint | Description | Auth |
|:---|:---|:---|:---|
| `GET` | `/complaints/:id/comments` | Get all comments for a grievance | ✅ |
| `POST` | `/complaints/:id/comments` | Add a comment to a grievance | ✅ |

### Health Check

| Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `/health` | Returns server status |

---

## 🔄 DevOps Pipeline

### Docker Compose Services

```yaml
services:
  db:        # PostgreSQL 15 Alpine — Port 5433
  backend:   # Node.js Express API — Port 5000
  frontend:  # React Vite App — Port 8080
```

### Jenkins CI/CD

The `Jenkinsfile` defines a 4-stage pipeline:

```
Checkout → Test Backend → Build Docker Images → Deploy to K8s
```

### Kubernetes Deployment

The `k8s/deployment.yaml` provisions:

| Resource | Replicas | Type |
|:---|:---|:---|
| `frontend-deployment` | 2 | LoadBalancer (port 8080) |
| `backend-deployment` | 2 | ClusterIP (port 5000) |

---

## 📂 Project Structure

```
nmims-grievance-portal/
│
├── backend/
│   ├── index.js                 # Express server entry point
│   ├── .env                     # Environment variables
│   ├── package.json
│   ├── Dockerfile
│   ├── lib/
│   │   └── prisma.js            # Prisma client singleton
│   ├── middleware/
│   │   └── authMiddleware.js    # JWT verification + RBAC
│   ├── routes/
│   │   ├── auth.js              # /api/auth (login, register)
│   │   └── complaints.js       # /api/complaints (CRUD, comments)
│   └── prisma/
│       ├── schema.prisma        # Database schema (4 models)
│       └── seed.js              # Admin account seeder
│
├── frontend/
│   ├── index.html
│   ├── vite.config.js
│   ├── tailwind.config.js
│   ├── package.json
│   ├── Dockerfile
│   └── src/
│       ├── App.jsx              # Router + Protected routes
│       ├── main.jsx             # React entry point
│       ├── context/
│       │   └── AuthContext.jsx  # JWT state management
│       ├── components/
│       │   ├── Navbar.jsx       # Top navigation bar
│       │   └── GrievanceDetail.jsx  # Detail modal + chat
│       └── pages/
│           ├── Login.jsx        # Sign in form
│           ├── Signup.jsx       # Registration form
│           ├── Dashboard.jsx    # Main grievance table + stats
│           └── SubmitGrievance.jsx  # New grievance form
│
├── k8s/
│   └── deployment.yaml          # K8s deployments + services
│
├── docker-compose.yml           # Multi-service orchestration
├── Jenkinsfile                  # CI/CD pipeline definition
└── README.md
```

---

## 📊 Database Schema

```mermaid
erDiagram
    USER ||--o{ COMPLAINT : submits
    USER ||--o{ COMPLAINT : "is assigned"
    USER ||--o{ COMMENT : writes
    USER ||--o{ AUDITLOG : performs

    COMPLAINT ||--o{ COMMENT : has
    COMPLAINT ||--o{ AUDITLOG : tracks

    USER {
        uuid id PK
        string name
        string email UK
        string password_hash
        enum role "USER | AUTHORITY | ADMIN"
        datetime createdAt
    }

    COMPLAINT {
        uuid id PK
        string category
        enum priority "LOW | MEDIUM | HIGH | CRITICAL"
        enum status "SUBMITTED | IN_PROGRESS | RESOLVED | CLOSED"
        string description
        boolean isAnonymous
        datetime slaDeadline
        uuid userId FK
        uuid assignedToId FK
    }

    COMMENT {
        uuid id PK
        string message
        datetime createdAt
        uuid complaintId FK
        uuid userId FK
    }

    AUDITLOG {
        uuid id PK
        string action
        datetime timestamp
        uuid complaintId FK
        uuid performedById FK
    }
```

---


This project was built as part of the **Agile & Prod. Development** course at SVKM's NMIMS.


