# LCIMS Docker Setup on your Local Computer

This repository contains the Docker Compose configuration to run the **Limbe City Information Management System (LCIMS)**. It includes the `backend`, `frontend`, and `PostgreSQL` database services, all built from pre-built Docker images.

---

## 🚀 Prerequisites

Before running the setup, make sure you have the following installed:

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

---

---

## 📦 Services Overview

### 1. Backend

- **Image**: `ejahdilan/lcims-backend:production`
- **Port**: `3000`
- **Environment Variables**:
    - `PORT=3000`
    - `DB_USER=${DB_USER}`
    - `DB_PASSWORD=${DB_PASSWORD}`
    - `DB_HOST=${DB_HOST}`
    - `DB_PORT=${DB_PORT}`
    - `DB_NAME=${DB_NAME}`
- **Depends On**: `db` (with health check)
- **Restart Policy**: `always`

---

### 2. Database

- **Image**: `ejahdilan/lcims-db:production`
- **Health Check**:
  - `pg_isready -U postgres`
- **Restart Policy**: `always`
- **Volumes**:
  - `postgres_data:/var/lib/postgresql/data` *(Persists PostgreSQL data)*

---

### 3. Frontend

- **Image**: `ejahdilan/frontend:production`
- **Port**: `8000` (Vite default)
- **Depends On**: `backend` (must be started)
- **Restart Policy**: `always`

---

## 🛠️ How to Run

### Step 1: Clone the Repository

```bash
git clone https://github.com/your-username/lcims_docker_setup.git

```

### Step 2: Get inside the repository folder

```bash
    
cd lcims_docker_setup

```

### Step 3: 🔐 Docker Login

To access the Docker images hosted on Docker Hub, you must log in with my Docker Hub username and a personal access token.

To log into my Docker Hub account use the command:

```bash
docker login -u ejahdilan
```

After running the command above you will prompted a PASSWORD use the token indicated below as the password

`
Visit the .env file to get the Access token to be able to pull the required images from Docker Hub
`

### Step 4: Start the Services

```bash
docker-compose up -d
```

### Step 5: Access the LCIMS Services

This services will start:

- The **backend** at [http://localhost:3000](http://localhost:3000)
- The **frontend** at [http://localhost:8000](http://localhost:8000)

### Step 6: Stop the Services

```bash
docker-compose down
```
