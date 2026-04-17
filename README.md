# 🐳 Docker Microservices with Custom Network

This project demonstrates how to build and run a simple microservices architecture using Docker, including custom networking and container communication.

---

## 📌 Project Overview

The project consists of:

* **Frontend service** (Python app)
* **Backend service** (Flask API)
* **Custom Docker network** for communication between containers

---

## 🧱 Architecture

* Two frontend containers:

  * `frontend1` (connected to custom network)
  * `frontend2` (default network)
* One backend container:

  * `backend` (connected to custom network)

👉 Only containers in the same network can communicate.

---

## ⚙️ Technologies Used

* Docker
* Python
* Flask
* Docker Networking

---

## 📁 Project Structure

```
.
├── frontend/
│   ├── app.py
│   ├── requirements.txt
│   └── Dockerfile
│
├── backend/
│   ├── app.py
│   └── Dockerfile
│
└── README.md
```

---

## 🐳 Docker Setup

### 1️⃣ Build Images

```bash
# Frontend
cd frontend
docker build -t frontend-image .

# Backend
cd ../backend
docker build -t backend-image .
```

---

### 2️⃣ Create Network

```bash
docker network create ivolve-network
```

---

### 3️⃣ Run Containers

```bash
# Backend
docker run -d --name backend --network ivolve-network backend-image

# Frontend 1 (connected to network)
docker run -d --name frontend1 -p 5006:5000 --network ivolve-network frontend-image

# Frontend 2 (default network)
docker run -d --name frontend2 -p 5007:5000 frontend-image
```

---

## 🔗 Communication Test

### ✅ Works (same network)

```bash
docker exec -it frontend1 curl http://backend:5000
```

### ❌ Fails (different network)

```bash
docker exec -it frontend2 curl http://backend:5000
```

---

## 🧠 Key Concepts

* Custom Docker networks enable **container-to-container communication**
* Containers can communicate using **container names as DNS**
* Default network does not allow easy name resolution

---

## 🧹 Cleanup

```bash
docker rm -f frontend1 frontend2 backend
docker network rm ivolve-network
```

---

## 📸 Screenshots (Optional)

*Add screenshots here if needed**

---

## ⭐ Notes

This project is part of hands-on Docker labs focused on:

* Containerization
* Networking
* Microservices basics
