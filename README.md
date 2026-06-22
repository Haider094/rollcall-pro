# RollCall Pro

A responsive, offline-capable web application for employee roll call and attendance tracking. Built for supervisors to conduct daily attendance on a tablet or laptop, eliminating paper attendance sheets.

**[Live Demo](https://haider094.github.io/rollcall-pro/)**

---

## Screenshots

**Upload Screen** — Upload your Excel schedule or load demo data instantly.
![Upload Screen](screenshots/upload.png)

**Roll Call Screen** — One-tap status buttons with live attendance stats and per-associate notes.
![Roll Call Screen](screenshots/rollcall.png)

**Complete Screen** — Summary modal with download and email options once all associates are marked.
![Complete Screen](screenshots/complete.png)

---

## Features

- **Excel Schedule Upload** — Upload `.xlsx` files exported from any scheduling system. Automatically parses associate names, IDs, routes, shifts, and wave assignments.
- **Auto Day Detection** — Detects today's day of the week and displays only associates scheduled to work that day. Manual override available.
- **One-Touch Roll Call** — Large, touch-friendly status buttons: Present, Late, Call Out, No Call No Show, Other.
- **Per-Associate Notes** — Add notes to any associate's record. Separate section for unscheduled attendees.
- **Live Stats** — Real-time summary of Present / Late / Absent / Pending counts.
- **Attendance Report** — Generates a complete `.xlsx` report on completion, including date, name, ID, route, status, notes, recorded-by, and timestamp.
- **Email Distribution** — Automatically emails the completed report to a configurable distribution list.
- **Offline Support** — Works without an internet connection via Service Workers and local storage. Data syncs automatically when connection is restored.
- **Backend Storage** — Saves all attendance records to a database for historical reporting.

---

## How It Works

1. Manager logs in and uploads the daily Excel schedule
2. App detects today's day and filters the roster automatically
3. Supervisor marks each associate's attendance status with one tap
4. On "Complete Roll Call," the app generates a report, emails it, and saves to the database
5. If offline, all data is saved locally and synced once connection is restored

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React (PWA) |
| Offline Support | Service Workers + IndexedDB |
| Excel Parsing | SheetJS (xlsx) |
| Report Generation | ExcelJS |
| Backend | Node.js + Express |
| Database | PostgreSQL |
| Email | Nodemailer (configurable SMTP) |
| Auth | JWT |

> This repository contains a **single-file HTML prototype** demonstrating the core UI and workflow. The full production build includes a Node.js backend, PostgreSQL database, email service, and offline sync engine.

---

## Running the Demo

No installation required. Open `index.html` directly in any browser.

1. Click **Load Demo Schedule** to populate a sample roster
2. Use the status buttons to mark each associate
3. Click **Complete Roll Call** to generate and download the attendance report

To test with your own Excel file, upload a `.xlsx` with columns: `Associate Name`, `Transporter ID`, `Route`, `Shift`, `Wave`, and day columns (`Monday`, `Tuesday`, etc.) with `1` or `Y` for scheduled days.

---

## Running the Full Stack Locally

### Prerequisites

- [Node.js](https://nodejs.org/) v18 or higher
- [PostgreSQL](https://www.postgresql.org/) v14 or higher
- An SMTP account for email (Gmail, SendGrid, etc.)

### 1. Clone the repository

```bash
git clone https://github.com/Haider094/rollcall-pro.git
cd rollcall-pro
```

### 2. Install dependencies

```bash
# Install backend dependencies
cd server
npm install

# Install frontend dependencies
cd ../client
npm install
```

### 3. Set up the database

```bash
# Create the database
psql -U postgres -c "CREATE DATABASE rollcall;"

# Run migrations
cd ../server
npm run migrate
```

### 4. Configure environment variables

Create a `.env` file inside the `server/` folder:

```env
PORT=4000
DATABASE_URL=postgresql://postgres:yourpassword@localhost:5432/rollcall
JWT_SECRET=your_secret_key_here

# Email config (example using Gmail)
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=you@gmail.com
SMTP_PASS=your_app_password
EMAIL_FROM=you@gmail.com
EMAIL_DIST_LIST=ops@company.com,hr@company.com
```

### 5. Start the backend

```bash
cd server
npm run dev
# Runs on http://localhost:4000
```

### 6. Start the frontend

```bash
cd client
npm run dev
# Runs on http://localhost:3000
```

Open `http://localhost:3000` in your browser. The app connects to the backend automatically.

---

## Production Deployment

The full production build supports:

- Secure login with role-based access (Supervisor / Manager / Admin)
- Multi-site support with separate rosters per location
- Historical attendance reporting and dashboards
- Configurable email distribution lists
- Automatic data backup

Deployment assistance included. Compatible with any cloud provider (AWS, Azure, GCP) or on-premise hosting.

---

## Contact

Built by a software engineer with experience delivering internal business tools for operations and logistics teams.
