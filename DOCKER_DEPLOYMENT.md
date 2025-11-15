# Docker Deployment Guide

## Prerequisites
- Docker installed: https://www.docker.com/products/docker-desktop
- Docker Compose installed (comes with Docker Desktop on Windows/Mac)

## Quick Start

### 1. Build and Start All Services
```bash
cd D:\Finalproject
docker-compose up -d
```

This will:
- Start MongoDB on port 27017
- Start Backend API on port 5001
- Start Frontend (Nginx) on port 80 (http://localhost)

### 2. Verify Services are Running
```bash
# Check all containers
docker-compose ps

# View backend logs
docker-compose logs backend

# View MongoDB logs
docker-compose logs mongodb
```

### 3. Access the Application
- **Frontend**: http://localhost
- **Backend API**: http://localhost:5001
- **Health Check**: http://localhost:5001/health
- **MongoDB**: localhost:27017 (internal only in containers)

### 4. Seed Database (Optional)
```bash
# Run seeder inside backend container
docker-compose exec backend node scripts/seedQuizzes.js
```

### 5. Stop All Services
```bash
docker-compose down
```

### 6. Clean Up (Remove volumes/data)
```bash
# WARNING: This deletes the MongoDB data
docker-compose down -v
```

## Environment Variables
Edit `docker-compose.yml` to change:
- `MONGO_URI`: MongoDB connection string
- `PORT`: Backend port
- `JWT_SECRET`: Change this to a strong secret
- `FRONTEND_ORIGINS`: Allowed frontend origins

## Deployment to VPS (DigitalOcean, AWS, etc.)
1. SSH into your VPS
2. Install Docker: `curl -fsSL https://get.docker.com -o get-docker.sh && sh get-docker.sh`
3. Clone your GitHub repo: `git clone https://github.com/keerthikonduru22/Hack_and_hired.git`
4. Navigate to project: `cd Hack_and_hired`
5. Run: `docker-compose up -d`
6. Access on your VPS IP address

## Troubleshooting
- **Port already in use**: Change ports in `docker-compose.yml` (e.g., `5002:5001`)
- **Container exits**: Check logs: `docker-compose logs [service_name]`
- **MongoDB won't start**: Ensure `/data/db` permissions or use named volumes (already configured)
