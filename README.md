## DevOps Setup

### Architecture
This project runs three containerized services:
- **frontend** — React + Vite app, built with a multi-stage Dockerfile (Node → Nginx)
- **backend** — .NET API, built with a multi-stage Dockerfile (SDK → runtime)
- **nginx** — Reverse proxy that routes traffic to frontend and backend

### Running Locally
docker compose up --build -d
- Frontend: http://localhost
- Backend health check: http://localhost/api/ping
- Port 80 is the only exposed port (via Nginx)

### CI/CD Pipeline
The GitHub Actions workflow (`.github/workflows/deploy-qa.yml`) triggers on every push to `main`. It builds and pushes Docker images to Docker Hub, then SSHs into the QA server to pull and redeploy.
