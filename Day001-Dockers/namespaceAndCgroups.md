# Linux Namespaces & Cgroups Guide

## 1. Introduction

Containers isolate processes on a shared host using core Linux kernel mechanisms:

* **Namespaces:** Provide process isolation.
* **Cgroups (Control Groups):** Enforce resource management and limits.

---

## 2. Kernel Architecture Flow

**Linux Kernel** ──> **Namespaces (Isolation)** ──> **Cgroups (Resource Control)** ──> **Container (Isolated + Controlled)**

---

## 3. Linux Namespaces

Namespaces restrict what a process can **see** by virtualization of system resources.

### Namespace Types

* **User Namespace:** Isolates user IDs and group IDs (`UID`/`GID` mapping).
* **PID Namespace:** Isolates process IDs (`PID 1` per container).
* **Network Namespace:** Isolates network interfaces, routing tables, and ports.
* **IPC Namespace:** Isolates inter-process communication (Shared Memory, System V IPC, POSIX message queues).
* **Mount Namespace:** Isolates filesystem mount points and view.
* **UTS Namespace:** Isolates hostname and NIS domain name.

### Isolation Model

**Host Machine** ──> **Linux Kernel** ──> **Namespaces** ──> [ **App A** | **App B** | **App C** ]

> **Note:** Each application runs in its own isolated view of system resources without knowing other processes exist on the host.

---

## 4. Control Groups (Cgroups)

Cgroups restrict how much a process can **use** across system resources.

### Resource Allocation Flow

**Process Group** ──> **Cgroup Controller** ──> **Resource Enforcement (CPU / Memory / Disk / Network)**

### Core Resource Limits

* **CPU:** Limits CPU shares, quotas, and core affinity (e.g., limit usage to **50%** of 1 core).
* **Memory:** Controls max RAM limit and OOM (Out-Of-Memory) kill triggers.
* **Disk I/O:** Controls block read/write speed and IOPS limits.
* **Network:** Manages egress/ingress traffic priority and bandwidth.

---

## 5. Namespaces vs Cgroups Comparison

| Mechanism | Main Purpose | Functional Role |
| :--- | :--- | :--- |
| **Namespaces** | **Process Isolation** | Controls **what** a container can see |
| **Cgroups** | **Resource Control** | Controls **how much** a container can use |

---

## Key Takeaways

* **Namespaces = Isolation** (Visibility Boundaries)
* **Cgroups = Resource Control** (Capacity Boundaries)
* **Together:** They form the foundational engine for modern containerization engines like Docker and containerd.