# day-11

# 🎮 Super Mario Mimic — Docker Deployment on VM

> Deploy a classic Super Mario web game using Docker on a cloud Virtual Machine.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [VM Setup](#vm-setup)
- [Docker Installation](#docker-installation)
- [Project Setup](#project-setup)
- [Build & Run](#build--run)
- [Access the Application](#access-the-application)
- [Firewall Configuration](#firewall-configuration)
- [Verify & Troubleshoot](#verify--troubleshoot)
- [Outcome](#outcome)

---

## Overview

This project demonstrates how to deploy a simple web-based Super Mario game using **Docker** on a **Virtual Machine (VM)** hosted on a cloud provider (GCP / AWS / Azure).

---

## Prerequisites

- A cloud account (GCP, AWS, or Azure)
- Basic familiarity with Linux terminal commands
- SSH access to your VM

---

## VM Setup

### 1. Create a VM Instance

- Go to your cloud provider console
- Create a **Linux VM** (Debian/Ubuntu recommended)
- Note the **External IP** of your VM for later

### 2. SSH into the VM / Open Cloud Shell

Update your package list:

```bash
sudo apt update
```

---

## Docker Installation

### Step 1 — Install Required Packages

```bash
sudo apt install ca-certificates curl
```

### Step 2 — Add Docker GPG Key

```bash
sudo install -m 0755 -d /etc/apt/keyrings

sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc

sudo chmod a+r /etc/apt/keyrings/docker.asc
```

### Step 3 — Add Docker Repository

```bash
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/debian
Suites: $(. /etc/os-release && echo "$VERSION_CODENAME")
Components: stable
Architectures: $(dpkg --print-architecture)
Signed-By: /etc/apt/keyrings/docker.asc
EOF
```

### Step 4 — Update Package List

```bash
sudo apt update
```

### Step 5 — Install Docker

```bash
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

---

## Project Setup

### 1. Clone the Repository

```bash
git clone https://github.com/iam-veeramalla/super-mario-mimic.git
```

### 2. Create a Dockerfile

```bash
vim Dockerfile
```

> Add your Dockerfile content, then save and exit with `:wq`

### 3. Move Dockerfile to Project Directory

```bash
cp Dockerfile super-mario-mimic/
```

### 4. Navigate to Project Directory

```bash
cd super-mario-mimic/
```

---

## Build & Run

### Build the Docker Image

```bash
docker build -t mario-game:v1 .
```

### Run the Docker Container

```bash
docker run -d -p 8080:8080 mario-game:v1
```

---

## Access the Application

Open your browser and navigate to your VM's External IP on port `8080`:

```
http://<EXTERNAL-IP>:8080
```

**Example:**

```
http://34.180.57.18:8080
```

---

## Firewall Configuration

> ⚠️ **Important:** If the app is not accessible, you need to open port `8080` in your cloud firewall.

### Steps (GCP Example)

1. Go to the **Cloud Console**
2. Navigate to **VPC Network → Firewall**
3. Click **Create Firewall Rule**
4. Configure the rule:

| Field | Value |
|---|---|
| **Name** | `allow-8080` |
| **Targets** | All instances (or your specific VM) |
| **Source IP ranges** | `0.0.0.0/0` |
| **Protocols and ports** | `tcp:8080` |

5. Click **Save**

---

## Verify & Troubleshoot

### Check Docker Service Status

```bash
sudo systemctl status docker
```

### List Running Containers

```bash
docker ps
```

### Confirm the App is Running

Open your browser and go to:

```
http://<EXTERNAL-IP>:8080
```

🎉 You should see the **Super Mario Game** running!

---

## Outcome

By completing this project, you have learned how to:

- ✅ Create and configure a cloud VM
- ✅ Install Docker on a Linux VM
- ✅ Build a custom Docker image
- ✅ Run and manage Docker containers
- ✅ Configure cloud firewall rules
- ✅ Deploy and access a web application on the cloud

---

## 📌 Resources

- [Docker Documentation](https://docs.docker.com/)
- [Super Mario Mimic Repository](https://github.com/iam-veeramalla/super-mario-mimic)
- [GCP Firewall Rules Guide](https://cloud.google.com/vpc/docs/firewalls)

---

> Made with ❤️ for learning Docker and cloud deployments.
