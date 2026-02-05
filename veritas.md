# 📘 Veritas Flow

**Veritas Flow** is a Fullstack project management system (SaaS) focused on productivity, collaboration, and security. The project evolved from a simple local Kanban to a robust application with authentication, teams, and protection against web vulnerabilities.

---

## 🚀 Main Features

### 1. Task Management (Kanban)
* **Fluid Drag & Drop:** Drag tasks between columns (To Do, In Progress, Done) with native touch support (Mobile).
* **Categorization:** Filters by Priority (High, Medium, Low) and Category (Dev, Design, Mkt, etc).
* **Smart Deadlines:** Automatic detection of overdue tasks with visual alerts.

### 2. Collaboration (New 👥)
* **Hybrid Mode:** Switch between **"Personal Board"** (only your tasks) and **"Team Board"** (shared tasks).
* **Assignment:** See who created the task on the visual card.

### 3. Authentication & Security (New 🛡️)
* **Secure Login:** Authentication via **JWT (JSON Web Token)**.
* **Data Protection:** Passwords encrypted with **Bcrypt**.
* **Anti-XSS Shield:** HTML input sanitization (backend) to prevent script injection.
* **Rate Limiting:** Protection against brute force and DDoS attacks (request per second limit).
* **Infrastructure:** Secure connection via SSL with cloud PostgreSQL database (Neon).

### 4. UX/UI & Mobile First
* **Responsive Design:** Layout that adapts to Mobile, Tablets, and Desktops.
* **Dark Mode:** Automatic/manual dark theme.
* **Drawer Menu:** Sliding sidebar for mobile devices.
* **Visual Feedback:** Success/error toasts and loading skeletons.

---

## 🛠️ Tech Stack

### Backend (Go)
* **Language:** Golang 1.23+
* **Web Server:** Gorilla Mux
* **ORM:** GORM
* **Database:** PostgreSQL (Production/Neon)
* **Security:**
    * `golang.org/x/crypto/bcrypt` (Password Hashing)
    * `golang-jwt/jwt` (Session Tokens)
    * `microcosm-cc/bluemonday` (HTML Sanitization)
    * `golang.org/x/time/rate` (Rate Limiter)

### Frontend (React)
* **Framework:** React.js
* **Styling:** Tailwind CSS
* **Interactivity:** `@dnd-kit/core` (Accessible Drag and Drop)
* **Global State:** React Context API (AuthContext)
* **Notifications:** `react-hot-toast`

---

## 📂 Project Structure

```text
desafio-fullstack-veritas/
├── backend/
│   ├── main.go            # Main entry point, Server Configuration, CORS and Rate Limiter
│   ├── handlers.go        # Route logic (CRUD, Sanitization and Team Filter)
│   ├── models.go          # Table definitions (User, Task) and Relationships
│   ├── auth.go            # Login, Registration and JWT generation logic
│   ├── go.mod             # Dependency manager
│   └── .env               # Environment variables (DO NOT COMMIT)
│
├── frontend/
│   ├── src/
│   │   ├── api.js         # Request hub (Automatically injects JWT Token)
│   │   ├── App.js         # Conditional routing (Login vs Kanban)
│   │   ├── index.css      # Tailwind configuration
│   │   ├── context/
│   │   │   └── AuthContext.js  # Manages logged user state
│   │   │
│   │   └── components/
│   │       ├── KanbanBoard.js    # Main Panel (Manages Solo/Team modes)
│   │       ├── TaskColumn.js     # Task column
│   │       ├── Task.js           # Task card (with author badge)
│   │       ├── TaskForm.js       # Creation modal (with "Share" checkbox)
│   │       ├── LoginPage.js      # Login and Registration screen
│   │       ├── StatsDashboard.js # Top metrics
│   │       ├── OverdueSidebar.js # Overdue drawer
│   │       └── ... (Other auxiliary components)
```

## Step 2: Setting up the Backend (API)
* **1. Navigate to the backend folder:**

```bash
cd backend
```

* **2. Create the security file: Create a file called .env in the root of the backend folder and fill it according to the template:**

```text
# Server Configuration
PORT=8080

# Security (Generate a strong random string)
JWT_SECRET=your_super_difficult_secret_key_here

# Database (Neon/Postgres link)
# Example: postgresql://user:pass@host/db?sslmode=require
DATABASE_URL="your_connection_string_here"
```

* **3. Install dependencies and run the server:**

```bash
go mod tidy
go run .
```

You should see the message: 🔒 ```SECURE Server running on port 8080...```

## Step 3: Setting up the Frontend (App)
* **1. Open a new terminal and navigate to the frontend folder:**

```bash
cd frontend
```

* **2. Install dependencies:**

```bash
npm install
```

* **3. Start the application:**

```bash
npm start
```

* **4. Access in your browser: ```http://localhost:3000```**

## 🔐 Security Implementation Details
To ensure the SaaS integrity, the following protection layers were applied:

* **1. HTML Sanitization:** All text input (Title, Description) goes through ```bluemonday.UGCPolicy()``` before touching the database. This removes dangerous tags like ```<script>```, ```<iframe>``` and ```onclick```.

* **2. Header Middlewares:** The server injects HTTP headers like ```X-XSS-Protection``` and ```X-Frame-Options``` in all responses.

* **3. Data Segregation:** The Backend validates the JWT Token in each request to ensure that users in "Personal" mode access strictly their own data.

## Developed with 💙 and lots of jazz playlists.
