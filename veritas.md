# 📘 Veritas Flow

<p align="center">
  <strong>Fullstack SaaS • Project Management • Security • Collaboration</strong>
</p>

**Status:** Completed

**Technologies:**
`Go` `React` `PostgreSQL` `JWT` `Tailwind CSS` `GORM`

---

## 🚀 Project Overview

**Veritas Flow** is a fullstack project management application designed around productivity, collaboration, responsive user experience and secure multi-user access.

The project evolved from a simple local Kanban board into a more complete SaaS-style application featuring:

* User authentication
* Personal and team workspaces
* Task ownership
* Persistent cloud data
* Security controls
* Responsive interfaces
* Real-time visual interaction
* Production-oriented backend architecture

The project demonstrates the evolution of a frontend prototype into a complete client-server application backed by a secure API and PostgreSQL database.

---

# 🎯 Project Evolution

The initial version of Veritas Flow focused primarily on local Kanban task management.

Over time, the architecture evolved to support authentication, persistent storage, collaboration and security.

```text id="vf-evolution"
Local Kanban
     ↓
Persistent Backend
     ↓
User Authentication
     ↓
PostgreSQL Database
     ↓
Personal Workspaces
     ↓
Team Collaboration
     ↓
Security Controls
     ↓
Responsive SaaS Application
```

This evolution required redesigning the project from a standalone task board into a multi-user system with clear separation between frontend, API and persistent data.

---

# ✨ Main Features

## 📋 Kanban Task Management

The main application experience is based on a Kanban workflow.

Tasks are organized across:

```text id="vf-kanban"
To Do
  ↓
In Progress
  ↓
Done
```

### Features

* Drag-and-drop task movement
* Touch support for mobile devices
* Task priority levels
* Task categories
* Deadline management
* Automatic overdue detection
* Visual alerts for delayed tasks

The interface uses `@dnd-kit/core` to provide accessible drag-and-drop interactions.

---

# 👥 Personal & Team Collaboration

Veritas Flow supports two working contexts.

## Personal Board

Displays tasks associated with the authenticated user.

This allows each user to maintain an independent workspace.

## Team Board

Displays tasks intended for collaboration.

Users can identify who created each shared task directly from the Kanban card.

```text id="vf-workspaces"
Authenticated User
        │
        ▼
   Workspace Mode
      /      \
     /        \
Personal      Team
Board         Board
  │             │
  ▼             ▼
Own Tasks   Shared Tasks
```

This required the backend to apply different filtering rules depending on the requested workspace.

---

# 🔐 Authentication

The application implements token-based authentication using **JSON Web Tokens (JWT)**.

The authentication workflow can be summarized as:

```text id="vf-auth"
User Credentials
       │
       ▼
Backend Authentication
       │
       ├── Validate User
       │
       └── Verify Password Hash
               │
               ▼
           JWT Issued
               │
               ▼
        React Application
               │
               ▼
    Authenticated API Requests
```

The frontend automatically includes the authentication token in protected API requests.

---

# 🔑 Password Security

Passwords are never intended to be stored in plaintext.

The backend uses **Bcrypt password hashing** through:

```text id="vf-bcrypt"
golang.org/x/crypto/bcrypt
```

During registration, the password is hashed before persistence.

During authentication, the submitted password is compared against the stored hash.

This provides a safer credential storage model than reversible encryption or plaintext password storage.

---

# 🛡️ Security Controls

Security was treated as an important architectural aspect of the project rather than an afterthought.

The backend includes multiple protection layers.

---

## 🧹 Input Sanitization

User-controlled textual fields such as task titles and descriptions are sanitized before being persisted.

The backend uses:

```text id="vf-blue"
bluemonday.UGCPolicy()
```

This helps reduce the risk of unsafe HTML being stored and later rendered by application clients.

Examples of potentially unsafe content include script elements, embedded frames and event-handler attributes.

---

## 🚦 Rate Limiting

The backend uses Go's rate-limiting utilities to control the frequency of incoming requests.

```text id="vf-rate"
golang.org/x/time/rate
```

This provides a protection layer against:

* Excessive request bursts
* Automated abuse
* Brute-force attempts
* Accidental client request loops

Rate limiting is an application-level defense and complements, rather than replaces, infrastructure-level traffic protection.

---

## 🧑‍💻 Data Segregation

Authentication alone is not enough in a multi-user system.

The API also verifies the authenticated user's identity when retrieving or modifying data.

In personal mode:

```text id="vf-isolation"
Request
   │
   ▼
Validate JWT
   │
   ▼
Identify User
   │
   ▼
Filter Database Query
   │
   ▼
Return Authorized Data
```

This prevents personal task data from simply being returned to every authenticated account.

---

## 🌐 Security Headers

The backend also sets HTTP response headers intended to improve browser-side security behavior.

These controls form an additional defensive layer around the API and frontend interaction.

---

# 🏛️ System Architecture

Veritas Flow follows a conventional fullstack client-server architecture.

```text id="vf-architecture"
┌─────────────────────────────┐
│       React Frontend        │
│                             │
│ Kanban                      │
│ Authentication              │
│ Dashboard                   │
│ Responsive UI               │
└──────────────┬──────────────┘
               │
               │ HTTP / JSON
               │ JWT
               ▼
┌─────────────────────────────┐
│          Go API             │
│                             │
│ Gorilla Mux                 │
│ Authentication              │
│ Authorization               │
│ Sanitization                │
│ Rate Limiting               │
│ Business Logic              │
└──────────────┬──────────────┘
               │
               │ GORM
               ▼
┌─────────────────────────────┐
│        PostgreSQL           │
│                             │
│       Neon Cloud DB         │
└─────────────────────────────┘
```

---

# ⚙️ Backend

The backend is implemented in **Go**, providing the application's API, authentication and business logic.

### Responsibilities

* HTTP routing
* User registration
* Authentication
* JWT generation and validation
* Task CRUD operations
* Workspace filtering
* Input sanitization
* Rate limiting
* Database communication

---

## Backend Stack

| Area                 | Technology               |
| -------------------- | ------------------------ |
| **Language**         | Go 1.23+                 |
| **HTTP Router**      | Gorilla Mux              |
| **ORM**              | GORM                     |
| **Database**         | PostgreSQL               |
| **Cloud Database**   | Neon                     |
| **Authentication**   | JWT                      |
| **Password Hashing** | Bcrypt                   |
| **Sanitization**     | Bluemonday               |
| **Rate Limiting**    | `golang.org/x/time/rate` |

---

# 🎨 Frontend

The frontend is built with React and provides the complete application interface.

### Responsibilities

* Authentication interface
* Kanban rendering
* Drag-and-drop interactions
* Workspace switching
* Task creation
* Filtering
* Dashboard metrics
* Responsive navigation
* Error and success feedback

---

## Frontend Stack

| Area                            | Technology        |
| ------------------------------- | ----------------- |
| **Framework**                   | React             |
| **Styling**                     | Tailwind CSS      |
| **Drag & Drop**                 | `@dnd-kit/core`   |
| **Global Authentication State** | React Context API |
| **Notifications**               | react-hot-toast   |

---

# 📱 Responsive UX

The application was designed to work across:

* Desktop
* Tablet
* Mobile

The interface adapts according to viewport size and includes mobile-oriented navigation behavior.

### UX Features

* Responsive layout
* Mobile drawer menu
* Touch-compatible drag and drop
* Dark mode
* Loading skeletons
* Success notifications
* Error notifications
* Visual deadline indicators

---

# 📊 Productivity Features

Beyond the main Kanban interface, the project includes additional productivity-oriented UI elements.

## Statistics Dashboard

Displays high-level task information and project metrics.

## Overdue Sidebar

Provides a dedicated view for tasks that have exceeded their deadlines.

## Filters

Tasks can be filtered according to attributes such as:

* Priority
* Category

These features reduce the need to manually inspect every task on the board.

---

# 📂 Project Structure

```text id="vf-tree"
desafio-fullstack-veritas/
├── backend/
│   ├── main.go
│   ├── handlers.go
│   ├── models.go
│   ├── auth.go
│   ├── go.mod
│   └── .env
│
└── frontend/
    ├── src/
    │   ├── api.js
    │   ├── App.js
    │   ├── index.css
    │   │
    │   ├── context/
    │   │   └── AuthContext.js
    │   │
    │   └── components/
    │       ├── KanbanBoard.js
    │       ├── TaskColumn.js
    │       ├── Task.js
    │       ├── TaskForm.js
    │       ├── LoginPage.js
    │       ├── StatsDashboard.js
    │       ├── OverdueSidebar.js
    │       └── ...
```

---

# 🧩 Separation of Responsibilities

The project separates application responsibilities across multiple layers.

```text id="vf-separation"
React Components
       ↓
Frontend State
       ↓
API Layer
       ↓
HTTP Backend
       ↓
Business Logic
       ↓
Database Access
       ↓
PostgreSQL
```

This structure makes the system easier to reason about than placing frontend, authentication, database and security logic into a single application layer.

---

# 🚀 Running the Project

## 1. Backend Configuration

Navigate to the backend:

```bash
cd backend
```

Create a `.env` file:

```env
PORT=8080

JWT_SECRET=replace_with_a_strong_random_secret

DATABASE_URL="postgresql://user:password@host/database?sslmode=require"
```

> Never commit `.env` files or production credentials to version control.

Install dependencies and start the API:

```bash
go mod tidy
go run .
```

---

## 2. Frontend Configuration

Open another terminal:

```bash
cd frontend
```

Install dependencies:

```bash
npm install
```

Start the application:

```bash
npm start
```

By default, the application can then be accessed locally through:

```text
http://localhost:3000
```

---

# ☁️ Database Infrastructure

The production-oriented configuration uses **PostgreSQL hosted on Neon**.

Connections are configured through the `DATABASE_URL` environment variable and use SSL when required by the database provider.

Using an external PostgreSQL service allowed the application to move beyond purely local persistence and operate with a cloud-hosted database.

---

# 🧠 Engineering Concepts Demonstrated

Veritas Flow provides practical experience with:

* Fullstack application architecture
* REST-style API development
* Authentication
* Authorization
* JWT-based sessions
* Password hashing
* PostgreSQL
* ORM-based persistence
* Cloud databases
* Input sanitization
* Application-level rate limiting
* Data isolation
* Responsive web interfaces
* Global frontend state
* Drag-and-drop interfaces
* Multi-user collaboration
* Environment-based configuration

---

# 📚 Key Learnings

One of the most important aspects of this project was understanding that adding authentication transforms the architecture of an application.

Once multiple users exist, the backend must consider not only:

> **"Is this user logged in?"**

but also:

> **"Does this user have permission to access this specific resource?"**

The project therefore strengthened my understanding of the distinction between:

```text id="vf-authz"
Authentication
      │
      └── Who is the user?

Authorization
      │
      └── What can this user access?

Data Isolation
      │
      └── Which records belong to this user?
```

Another important lesson was that application security should exist across multiple layers rather than relying on a single mechanism.

---

# 🔭 Future Possibilities

The architecture could be expanded with features such as:

* Organization-level workspaces
* Fine-grained project permissions
* Task comments
* Activity history
* Invitations
* Refresh tokens
* Email verification
* Automated testing
* CI/CD pipelines
* Containerized deployment
* Observability and logging
* Audit trails
* Real-time collaboration

These additions could move the system closer to a production-grade collaborative SaaS platform.

---

# 📌 Project Summary

**Veritas Flow** represents the transition from a simple frontend productivity tool into a complete multi-user fullstack system.

Technically, the project combines:

```text id="vf-summary"
React
  ↓
Authenticated API
  ↓
Go Backend
  ↓
Authorization & Security
  ↓
GORM
  ↓
PostgreSQL / Neon
```

The project demonstrates practical knowledge of **backend development, frontend architecture, authentication, data security, relational persistence and SaaS-style application design**.

---

<p align="center">
  <i>Building software that is not only functional, but structured, secure and ready to evolve.</i>
</p>
