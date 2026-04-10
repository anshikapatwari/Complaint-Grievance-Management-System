# NMIMS Grievance Portal - Project Documentation

This document provides a complete overview of the **Advanced Project Development (APD)** grievance management system, detailing its architecture, technologies, and features.

---

## 🏗️ 1. Project Architecture
The system follows a classic **Full-Stack (PERN)** architecture, optimized for security, scalability, and modern "WOW" aesthetics.

- **Frontend**: A React-based Single Page Application (SPA) with a glassmorphic NMIMS-branded design.
- **Backend**: A robust RESTful API powered by Node.js and Express.
- **Database**: A relational PostgreSQL database managed via Prisma ORM for type-safety and efficient querying.
- **Environment**: Containerized database via Docker for easy setup and isolation.

---

## 🛠️ 2. Technology Stack & Tools

### **Backend (The Core Engine)**
| Tool | Purpose | Role in this Project |
| :--- | :--- | :--- |
| **Node.js** | Runtime Environment | Executes Javascript code on the server side. |
| **Express** | Web Framework | Handles API routing and middleware (Auth, CORS, JSON parsing). |
| **Prisma ORM** | Database Layer | Bridges the gap between Javascript and PostgreSQL—handles migrations and queries. |
| **Bcryptjs** | Security | Hashes (encrypts) user passwords before they are stored in the database. |
| **JSON Web Token (JWT)** | Authentication | Creates secure, encrypted "tokens" to verify when a user is logged in. |

### **Frontend (The User Interface)**
| Tool | Purpose | Role in this Project |
| :--- | :--- | :--- |
| **React** | JS Library | Powers the interactive components and state management (e.g., the Chat Modal). |
| **Vite** | Build Tool | Extremely fast development server and build pipeline. |
| **Tailwind CSS v4** | Styling | Provides the modern, premium NMIMS branding and glassmorphic effects. |
| **Lucide Icons** | Visual Assets | Professional, thin-line icons used across the dashboard and forms. |
| **Axios** | API Client | Handles all communication between the browser and the backend server. |

### **Infrastructure & DevOps**
| Tool | Purpose | Role in this Project |
| :--- | :--- | :--- |
| **Docker** | Containerization | Runs the PostgreSQL database in an isolated "container," ensuring it works on any laptop. |
| **PostgreSQL** | Database | Stores all permanent data (Users, Grievances, Comments, Audit Logs). |
| **VS Code** | IDE | The primary development environment used to write and debug all code. |

---

## 🌟 3. Key Features Delivered

### **🛡️ Advanced Authentication**
- **Student Sign-Up**: Interactive registration flow with form validation.
- **Admin Seeder**: A hardcoded script (`npx prisma db seed`) that instantly creates a "Professor/Admin" account for testing.
- **Role-Based Access (RBAC)**: Different dashboards and permissions for `USER`, `AUTHORITY`, and `ADMIN`.

### **📋 Grievance Management & Lifecycle**
- **SLA Engine**: Automatically calculates a "Resolution Deadline" based on the problem's priority.
- **Priority Privacy**: Students can submit issues without being bothered by administrative complexity—priority and SLA are strictly managed by Admins.
- **Audit Logs**: Every single change (Status update, Priority change, Comment) is saved in a permanent record for accountability.

### **💬 Real-Time Communication (Grievance Chat)**
- **Timeline Discussion**: A new "Chat" system where students and authorities can talk, ask for updates, or provide evidence.
- **Detail View**: A premium modal that centralizes all information (Description, Progress, Timeline) in one place.

---

## 🎯 4. Summary of Improvements
We transformed a static application into a **premium, role-driven portal** that is ready for production. 

---
© 2026 SVKM's NMIMS MPSTME. Built for Advanced Project Development.
