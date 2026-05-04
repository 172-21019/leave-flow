# 🏖️ LeaveFlow — Employee Leave Management System
### DevOps Mini Project | Node.js + Git + Jenkins + Docker

---

## 📌 Overview
LeaveFlow is a full-stack Employee Leave Management System with two roles — Employee and Manager — built with Node.js (Express) and deployed via a complete CI/CD pipeline.

---

## 🏗️ Tech Stack
| Layer | Technology |
|-------|-----------|
| Backend | Node.js + Express |
| Frontend | HTML, CSS, JS |
| Testing | Jest + Supertest |
| Container | Docker + Docker Compose |
| CI/CD | Jenkins Pipeline |
| VCS | Git + GitHub |
| Proxy | Nginx |

---

## 👥 Roles
| Role | Capabilities |
|------|-------------|
| Employee | Apply leave, view balance, cancel pending, view history |
| Manager | View all leaves, approve/reject with comments, view history |

---

## 📁 Project Structure
```
leave-manager/
├── src/app.js           # Express REST API
├── public/index.html    # Frontend UI
├── tests/app.test.js    # Jest unit tests
├── Dockerfile
├── docker-compose.yml
├── Jenkinsfile
├── nginx.conf
└── package.json
```

---

## 🔌 REST API Endpoints
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | /api/employees | Get all employees |
| GET | /api/employees/:id | Get employee by ID |
| GET | /api/leaves | Get leaves (filterable) |
| POST | /api/leaves | Apply for leave |
| PUT | /api/leaves/:id/action | Approve or reject leave |
| PUT | /api/leaves/:id/cancel | Cancel leave |
| GET | /api/stats | Get dashboard stats |
| GET | /health | Health check |

---

## 🚀 How to Run

### Locally
```bash
npm install
node src/app.js
# Open http://localhost:3000
```

### With Docker
```bash
docker build -t leave-manager .
docker run -p 3000:3000 leave-manager
```

### With Docker Compose
```bash
docker-compose up -d
```

---

## 🔄 Jenkins CI/CD Pipeline
```
Checkout → Install → Test → Audit → Docker Build → Push → Deploy → Health Check
```

---

## ✨ Features
- ✅ Employee & Manager login (role-based UI)
- ✅ Apply, approve, reject, cancel leaves
- ✅ Leave balance tracking (Casual / Sick / Earned)
- ✅ Dashboard with live stats
- ✅ Full leave history with filters
- ✅ REST API with health check
- ✅ Dockerized + Jenkins CI/CD

---
DevOps Mini Project — LeaveFlow
