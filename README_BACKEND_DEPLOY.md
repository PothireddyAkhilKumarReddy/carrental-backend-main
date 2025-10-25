# Backend Docker deployment (local)

This document explains how to run the backend using Docker Compose with a persistent MySQL volume and how to verify signup/login endpoints.

Prerequisites:
- Docker and Docker Compose installed
- Java/Maven if you want to run locally without Docker

Run locally with Docker Compose:

1. From the project root run:

```powershell
docker compose up --build -d
```

2. Confirm containers are running:

```powershell
docker compose ps
```

3. Check logs:

```powershell
docker compose logs -f backend
```

4. Backend will be reachable at: http://localhost:8081

Verify signup/login (example using curl):

Signup:

```powershell
curl -X POST http://localhost:8081/auth/signup -H "Content-Type: application/json" -d '{"username":"testuser","password":"testpass","email":"test@example.com"}'
```

Login:

```powershell
curl -X POST http://localhost:8081/auth/login -H "Content-Type: application/json" -d '{"username":"testuser","password":"testpass"}'
```

Data persistence:
- The MySQL data is stored in a named Docker volume `carrental_mysql_data`. Stopping and removing containers will keep the DB data.

CI notes:
- A GitHub Actions workflow `backend-ci.yml` is included. Configure `REGISTRY` and `PUSH_IMAGE` secrets to push Docker images to your container registry.
