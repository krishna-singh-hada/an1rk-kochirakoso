# Docker Setup & Container Registries Guide

## 1. Docker Linux Setup

### Installation Workflow
**Linux System** ──> **Update Packages** ──> **Install Docker** ──> **Configure User & Group** ──> **Check Processes** ──> **Manage Images** ──> **Run Containers**

### Essential System Commands
* **Update Packages:** `sudo apt update`
* **Install Docker:** `sudo apt install docker.io`
* **Manage Service:** 
  * `sudo systemctl start docker` (Start)
  * `sudo systemctl enable docker` (Enable on boot)
  * `sudo systemctl status docker` (Check status)
* **Grant Access:** `sudo usermod -aG docker $USER` *(Requires re-login)*

> **Note:** **Ubuntu/Debian** uses `docker.io` as the official package name.

---

## 2. Linux & Docker Basic Commands

### System Architecture Flow
**User / Group Permissions** ──> **Docker Process Access** ──> **Running Containers**

### System Inspection
* **Current User:** `whoami`
* **User Groups:** `groups`
* **View Processes:** `ps` | `ps aux`
* **Create User/Group:** `sudo useradd <name>` | `sudo groupadd <name>`

### Docker Verification
* **System Info:** `docker --version` | `docker info`
* **List Containers:** `docker ps` *(Active)* | `docker ps -a` *(All)*
* **List Images:** `docker images` | `docker image ls`

---

## 3. Container Registries & Docker Hub

### Registry Workflow
**Docker Image** ──> **Container Registry / Docker Hub** ──(**Pull/Push**)──> **Docker Host** ──> **Running Container**

### Popular Registries
* **Public:** Docker Hub
* **Enterprise / On-Prem:** Harbor, JFrog Artifactory, Quay.io
* **Cloud Native:** AWS ECR, Azure Container Registry (ACR), Google Artifact Registry (GAR), GitHub Packages

### Docker Hub Image Categories
* **Official Images:** High-quality , security-scanned base images.
* **Verified Publisher:** Maintained by certified commercial vendors.
* **Sponsored OSS:** Community open-source projects supported by Docker.
* **User/Org:** Custom repositories published by individuals or companies.

### Image Tagging Strategy
* **Examples:** `nginx:1.26`, `nginx:1.26.0`, `nginx:stable`, `nginx:latest`
* **Best Practice:** Avoid relying solely on `:latest` in production environments. Explicitly tag images with exact semantic versions to ensure idempotent deployments.

---

## 4. Complete Lifecycle Commands

### Command Lifecycle
**Build** ──> **Tag** ──> **Push** ──> **Registry** ──> **Pull** ──> **Run**

### Image Management
* **Search Registry:** `docker search <query>`
* **Pull Image:** `docker pull <image>:<tag>`
* **Inspect Metadata:** `docker image inspect <image>`
* **View Layer History:** `docker image history <image>`
* **Tag Image:** `docker tag <source> <repository>:<tag>`
* **Remove Image:** `docker image rm <image>`
* **Clean Unused Images:** `docker image prune -a`

### Local Execution Workflow
1. **Build:** `docker build -t my-app:1.0 .`
2. **Push:** `docker push username/my-app:1.0`
3. **Pull:** `docker pull username/my-app:1.0`
4. **Run:** `docker run -d username/my-app:1.0`

---

## Key Takeaways
* **Image:** Read-only template containing application code and dependencies.
* **Container:** Isolated, runnable instance of an image.
* **Tag:** Version identifier assigned to an image repository.
* **Registry:** Storage hub used to store, share, and distribute container images.
