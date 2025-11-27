# MEAN CRUD App — Containerized & CI/CD

## Overview
This repository contains a MEAN (MongoDB, Express, Angular, Node.js) CRUD application and all configuration to containerize and deploy it to an Ubuntu VM using Docker Compose. CI/CD is implemented with GitHub Actions, which builds and pushes Docker images to Docker Hub and remotely deploys to the VM.

## Repo structure
- `backend/` — Node.js Express backend
- `frontend/` — Angular frontend
- `backend/Dockerfile` — Dockerfile for backend
- `frontend/Dockerfile` — Dockerfile for frontend (multi-stage build with nginx)
- `docker-compose.yml` — development or local compose
- `docker-compose-prod.yml` — production compose for the VM (pulls images)
- `.github/workflows/ci-cd.yml` — GitHub Actions workflow

## Requirements
- GitHub repository
- Docker Hub account
- Ubuntu VM (AWS/Azure/GCP/other)
- Docker & Docker Compose installed on VM
- GitHub Secrets (detailed below)

## Setup steps (local + push to GitHub)
1. Create a new GitHub repo and push entire project (including the Dockerfiles and workflow).
2. Create Docker Hub repository names: `<your-username>/crud-backend` and `<your-username>/crud-frontend`.
3. Create GitHub Secrets:
   - `DOCKERHUB_USERNAME`
   - `DOCKERHUB_TOKEN`
   - `VM_HOST`
   - `VM_USER`
   - `VM_SSH_PORT`
   - `VM_SSH_PRIVATE_KEY`
4. Push code to `main`. GitHub Actions will build & push the images.

## VM setup (Ubuntu)
1. Create VM (e.g., t2.micro on AWS).
2. SSH into VM and run:
```bash
# update and install docker
sudo apt update && sudo apt upgrade -y
sudo apt install -y ca-certificates curl gnupg lsb-release
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin
# add your user to docker group (logout/login required)
sudo usermod -aG docker $USER

