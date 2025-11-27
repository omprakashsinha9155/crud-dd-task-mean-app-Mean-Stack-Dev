**MEAN CRUD App — Containerized & CI/CD 🚀**

📌 Overview
This repository contains a **"MEAN stack (MongoDB, Express, Angular, Node.js)"** CRUD application, fully containerized and configured for deployment on an **"Ubuntu VM"** using 
Docker Compose.  
CI/CD is implemented with "GitHub Actions", which automatically builds and pushes Docker images to **"Docker Hub"**, then remotely deploys them to the VM.

📂 **Repository Structure**
- backend — Node.js Express backend  
- frontend — Angular frontend  
- backend/Dockerfile — Dockerfile for backend  
- frontend/Dockerfile — Dockerfile for frontend (multi-stage build with nginx)  
- docker-compose.yml — Local development compose file  
- docker-compose-prod.yml — Production compose file (pulls images from Docker Hub)  
- .github/workflows/ci-cd.yml — GitHub Actions workflow for CI/CD  

✅ **Requirements**
- GitHub repository  
- Docker Hub account  
- VM (Ubuntu recommended, but Windows Server is possible with Docker Desktop/WSL2)  
- Docker & Docker Compose installed on VM  
- GitHub Secrets configured (see below)  

⚙️ **Setup Steps (Local + Push to GitHub)**
1. Create a new GitHub repository and push the entire project (including Dockerfiles and workflow).  
2. Create Docker Hub repositories:  
   - `<your-username>/crud-backend`  
   - `<your-username>/crud-frontend`  
3. Configure GitHub Secrets:  
   - `DOCKERHUB_USERNAME`  
   - `DOCKERHUB_TOKEN`  
   - `VM_HOST`  
   - `VM_USER`  
   - `VM_SSH_PORT`  
   - `VM_SSH_PRIVATE_KEY`  
4. Push code to the `main` branch.  
   - GitHub Actions will build & push the images to Docker Hub.  

🖥️ **VM Setup (Ubuntu)**
1. Create an Ubuntu VM (e.g., **t2.micro on AWS**).  
2. SSH into the VM and install Docker & Docker Compose:

```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Install prerequisites
sudo apt install -y ca-certificates curl gnupg lsb-release

# Add Docker’s official GPG key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Set up stable repository
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Install Docker & Compose
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin

# Add your user to docker group (logout/login required)
sudo usermod -aG docker $USER
```


🖥️ **VM Setup (Windows Alternative)**
If you prefer a **Windows VM**:
- Install **Docker Desktop** or **Docker Engine for Windows Server**.  
- Ensure **WSL2** is enabled for Linux container support.  
- Adapt installation commands (use PowerShell/Chocolatey instead of `apt-get`).  
- The CI/CD pipeline remains the same, but Docker commands will run in PowerShell.


 🚀 **Deployment**
- Once GitHub Actions completes successfully, the VM will automatically pull the latest images and run them using `docker-compose-prod.yml`.  
- You can verify containers with:  

```bash
docker ps
```


🎯 **Features**
- Full-stack MEAN CRUD functionality  
- Containerized backend & frontend  
- Multi-stage Angular build with nginx  
- Automated CI/CD pipeline with GitHub Actions  
- Remote deployment to VM (Ubuntu recommended, Windows possible)  


👨‍💻 **About me**
Hi, I'm Om Prakash Sinha a Computer Science & Engineering graduate from Sandip University.  
  
- 💼 LinkedIn: https://www.linkedin.com/in/om-prakash-sinha/ 
- 📧 Email: omprakashsinha9155@gmail.com 

