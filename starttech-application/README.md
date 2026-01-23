# StartTech Application

This repository contains the source code for the StartTech full-stack application.

- **Frontend**: React application (located in `frontend/`)
- **Backend**: Go API (located in `backend/`)

## CI/CD Pipelines

Pipelines are defined in `.github/workflows/`.

### Frontend Pipeline (`frontend-ci-cd.yml`)

- Triggers on push to `frontend/`
- Builds React app
- Deploys to S3
- Invalidates CloudFront cache

### Backend Pipeline (`backend-ci-cd.yml`)

- Triggers on push to `backend/`
- Runs Go tests and linters
- Builds Docker image and pushes to ECR
- Refreshes ASG instances to deploy new image

## Local Development

### Frontend

```bash
cd frontend
npm install
npm run dev
```

### Backend

```bash
cd backend
go run cmd/server/main.go
```
