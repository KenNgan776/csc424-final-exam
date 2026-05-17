# CSC424 Final Exam — Containerized Web Application

## DevOps Setup

### Running the stack locally

```bash
docker compose up --build -d
```

### URLs to test

- **Frontend:** http://localhost
- **Backend:** http://localhost/api/ping

### Services

- **frontend** — React + Vite app served by Nginx on port 80
- **backend** — .NET 10 Web API serving the /api/ping endpoint on port 8080
- **nginx** — Reverse proxy that routes / to the frontend and /api/ to the backend. Only nginx is exposed to the host on port 80.

### CI/CD Pipeline

On every push to `main`, GitHub Actions:
1. Builds the frontend and backend Docker images
2. Pushes both images to Docker Hub
3. SSHs into the QA server and runs `docker compose up -d` to deploy the latest images

All credentials are stored as GitHub Secrets — nothing is hardcoded.
