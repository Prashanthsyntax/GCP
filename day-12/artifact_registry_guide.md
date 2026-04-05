# 🚀 End-to-End Guide: Google Cloud Artifact Registry

## 📌 Objective
- Build a Docker image  
- Tag the image  
- Push it to Artifact Registry  

---

## 🧱 Step 1: Set Environment Variables

```bash
export PROJECT_ID="docker-demo-492317"
export REGION="asia-south1"
export ZONE="asia-south1-a"
export REPO="e-commerce-payments-dev"
export IMAGE="payments-demo"
export TAG="v1"

export AR_HOST="${REGION}-docker.pkg.dev"
export IMG_PATH="${AR_HOST}/${PROJECT_ID}/${REPO}/${IMAGE}"
```

---

## 🐳 Step 2: Install Docker

```bash
sudo apt-get update -y
sudo apt install -y docker.io
```

```bash
sudo systemctl start docker
sudo systemctl enable docker
```

```bash
sudo usermod -aG docker $USER
newgrp docker
```

```bash
docker --version
```

---

## 📄 Step 3: Create Dockerfile

```bash
vim Dockerfile
```

```Dockerfile
FROM nginx:1.27-alpine
RUN echo 'Hello from Artifact Registry!' > /usr/share/nginx/html/index.html
```

---

## 🏗️ Step 4: Build Docker Image

```bash
docker build -t ${IMAGE}:local .
```

```bash
docker images
```

---

## 🏷️ Step 5: Tag Image

```bash
docker tag <IMAGE_ID> ${IMG_PATH}:${TAG}
```

Example:

```bash
docker tag 6c742d279587 ${IMG_PATH}:${TAG}
```

---

## 🔐 Step 6: Authenticate Docker

```bash
gcloud auth configure-docker ${AR_HOST}
```

---

## 📤 Step 7: Push Image

```bash
docker push ${IMG_PATH}:${TAG}
```

---

## 🧠 Workflow

Dockerfile → docker build → docker tag → authenticate → docker push

---

## 🔥 Architecture

- Docker → Build image  
- Artifact Registry → Store image  
- VM / Kubernetes → Pull and run  

---

## ⚠️ Errors & Fixes

### docker: command not found
```bash
sudo apt install -y docker.io
```

### permission denied
```bash
sudo usermod -aG docker $USER
newgrp docker
```

### Unauthenticated request
```bash
gcloud auth configure-docker
```

---

## 🎯 Use Case

- Build image using CI/CD  
- Push to Artifact Registry  
- Deploy using VM or Kubernetes  
