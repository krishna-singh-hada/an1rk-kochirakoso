# Docker Architecture Guide

## 1. Introduction

Docker operates on a **client-server architecture**. The **Docker CLI** sends REST API commands to the **Docker Daemon**, which orchestrates container operations and delegates low-level execution down to **containerd** and **runc**.

---

## 2. Architecture Execution Flow

**Docker CLI** *(User Commands)* ──> **Docker Daemon** *(Engine / Object Manager)* ──> **Containerd** *(Lifecycle Coordinator)* ──> **Runc** *(OCI Low-Level Runtime)* ──> **Linux Kernel** *(Namespaces & Cgroups)* ──> **Running Container** *(Isolated Process)*

---

## 3. Docker Daemon Core Responsibilities

The **Docker Daemon (`dockerd`)** manages primary system objects and infrastructure integrations:

### Managed Docker Objects
* **Images:** Read-only application templates.
* **Containers:** Active, runnable instances of images.
* **Networks:** Internal/external container communication bridges.
* **Volumes:** Persistent data storage decoupled from container lifecycles.

### Engine Operations
* **Security:** User authentication, authorization, and permission checks.
* **Lifecycle:** Processing container creation, destruction, and monitoring requests.
* **Storage & Network:** Image layer management, volume mounting, and network driver configuration.
* **Maintenance:** Automatic garbage collection of dangling resources.

---

## 4. Container Run Execution Order (`docker run`)

1. **CLI:** Receives `docker run` command and sends an API request to the Daemon socket.
2. **Daemon:** Verifies image availability (pulls from registry if missing), sets up networks and storage mounts.
3. **Containerd:** Receives request from Daemon, sets up bundle, and coordinates execution lifecycle.
4. **Runc:** Interacts directly with kernel features (*Namespaces/Cgroups*) to create and start the container process.
5. **Monitoring:** **Runc** exits after launch; **Containerd** takes over process supervision and monitoring.

---

## 5. Architectural Components Breakdown

| Component | Layer / Role | Primary Function |
| :--- | :--- | :--- |
| **Docker CLI** | **Client** | User interface for issuing commands |
| **Docker Daemon (`dockerd`)** | **High-Level Engine** | Object management, API endpoint, security, orchestration |
| **Containerd** | **High-Level Runtime** | Image distribution, execution coordination, process supervision |
| **Runc** | **Low-Level Runtime** | OCI-compliant container creation and kernel configuration |
| **Container** | **Runtime Process** | The actual isolated application running on the Linux host |

---

## 6. Practical Example: Flask Web Application

### Deployment Commands

* **Build Image:** `docker build -t flask-app .`
* **Run Container:** `docker run -p 5000:5000 flask-app`
* **List Containers:** `docker ps`
* **Stop Container:** `docker stop <container_id_or_name>`

---

## Key Takeaway

**CLI** ──> **Daemon** ──> **Containerd** ──> **Runc** ──> **Linux Kernel** ──> **Container**

> **Modular Design:** Docker separates management (*Daemon*), supervision (*Containerd*), and execution (*Runc*) into distinct decoupled layers for reliability and adherence to open container standards (OCI).