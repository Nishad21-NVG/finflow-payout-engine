# FinFlow Payout Engine 🚀

A production-ready fintech payout management platform built with React, Django, PostgreSQL, Redis, and Docker.  
This project simulates secure merchant payout workflows with transaction tracking, approval systems, retry mechanisms, and concurrency-safe ledger operations.

---

## ✨ Features

### 🔐 Secure Transaction Handling
- Database-level locking using `select_for_update()`
- Prevents race conditions and double withdrawals
- Atomic transaction processing

### 💳 Dynamic Ledger System
- Append-only ledger architecture
- Balance computed using:
  ```python
  SUM(credits) - SUM(debits)
  ```
- Eliminates floating-point inconsistencies

### ⚡ Idempotent API Requests
- Duplicate payout requests automatically rejected
- UUID-based request tracking
- Safe retry support for network failures

### 🔄 Background Retry Engine
- Celery worker integration with Redis
- Simulated payout processing pipeline
- Exponential retry mechanism for failed payouts

### 📊 Admin Approval Workflow
- Admin dashboard for transaction review
- Approve / Reject payout requests
- Live transaction status updates

### 🐳 Dockerized Infrastructure
- PostgreSQL containerized setup
- Redis service orchestration
- One-command local startup using Docker Compose

---

# 🛠️ Tech Stack

| Layer | Technology |
|-------|------------|
| Frontend | React + Vite |
| Backend | Django |
| Database | PostgreSQL |
| Queue/Cache | Redis |
| Async Tasks | Celery |
| Containerization | Docker |
| ORM | Django ORM |

---

# 📂 Project Structure

```bash
finflow-payout-engine/
│
├── frontend/              # React frontend
├── core/                  # Django app
├── playto_payouts/        # Django settings
├── docker-compose.yml
├── manage.py
├── requirements.txt
└── seed.py
```

---

# ⚙️ Local Setup

## 1️⃣ Start Docker Services

```bash
docker compose up -d
```

Starts:
- PostgreSQL
- Redis

---

## 2️⃣ Setup Backend

### Create Virtual Environment

```bash
python -m venv venv
```

### Activate Environment

#### Windows
```bash
venv\Scripts\activate
```

#### Linux/Mac
```bash
source venv/bin/activate
```

### Install Dependencies

```bash
pip install -r requirements.txt
```

### Run Database Migrations

```bash
python manage.py makemigrations
python manage.py migrate
```

### Seed Demo Data

```bash
python seed.py
```

### Start Django Server

```bash
python manage.py runserver
```

Backend:
```bash
http://127.0.0.1:8000
```

Admin Panel:
```bash
http://127.0.0.1:8000/admin
```

---

# ⚡ Run Celery Worker

Open a new terminal:

```bash
venv\Scripts\activate
celery -A playto_payouts worker -l info --pool=solo
```

> `--pool=solo` is recommended on Windows.

---

# 🎨 Frontend Setup

```bash
cd frontend
npm install
npm run dev
```

Frontend:
```bash
http://localhost:5173
```

---

# 🧪 Running Tests

```bash
python manage.py test core
```

Tests include:
- Concurrency validation
- Idempotency verification
- Transaction safety checks

---

# 🚀 Deployment

## Deploy Backend

1. Push repository to GitHub
2. Create new Railway project
3. Connect GitHub repository
4. Add:
   - PostgreSQL plugin
   - Redis plugin
5. Configure:
   - `DATABASE_URL`
   - `REDIS_URL`

---

## Deploy Frontend

Create separate frontend service:

```bash
Root Directory: /frontend
```

---

# 🔥 Core Functionalities

- Merchant payout processing
- Transaction ledger system
- Background payout retries
- Admin-controlled approvals
- Real-time status updates
- Redis queue integration
- PostgreSQL transactional integrity

---

# 📸 Preview

## Dashboard Features
- Available balance tracking
- Held processing balance
- Withdrawal request system
- Transaction history table
- Pending / Approved / Rejected statuses

---

# 👨‍💻 Author

### Nishad Ghatage

B.Tech CSE Student | Full Stack Developer | AI & Fintech Enthusiast

GitHub:
https://github.com/Nishad21-NVG

---

# ⭐ Future Improvements

- JWT Authentication
- Razorpay/Stripe Integration
- WebSocket Real-Time Updates
- Email Notifications
- Analytics Dashboard
- Multi-Merchant Support
- Role-Based Access Control

---

# 📄 License

This project is intended for educational and portfolio purposes.
