# MERN Stack Deployment with Kubernetes, Helm & Jenkins

This project automates the deployment of a MERN (MongoDB, Express.js, React.js, Node.js) stack application using **Docker**, **Kubernetes (Minikube)**, **Helm**, and **Jenkins Groovy pipeline**.

---

## 📁 Project Structure

```bash
mern-k8s-helm-jenkins/
│
├── learnerReportCS_frontend/     # React frontend
├── learnerReportCS_backend/      # Express backend
├── mern-chart/                   # Helm chart
│   ├── templates/
│   ├── values.yaml
│   └── Chart.yaml
└── Jenkinsfile                   # Groovy pipeline (WIP)
```

# 🐳 Docker Setup
## Build and Push Docker Images
```bash
# Frontend
docker build -t mern-frontend ./learnerReportCS_frontend
docker tag mern-frontend shakti827/mern-frontend:latest
docker push shakti827/mern-frontend:latest
```
### Screenshots
<img width="1048" height="429" alt="image" src="https://github.com/user-attachments/assets/fa057c5f-4ef2-4386-98db-3b474533b635" />
<img width="976" height="392" alt="image" src="https://github.com/user-attachments/assets/e047cd0c-4f64-4e95-9843-c7834bff8bb4" />


---

```bash
# Backend
docker build -t mern-backend ./learnerReportCS_backend
docker tag mern-backend shakti827/mern-backend:latest
docker push shakti827/mern-backend:latest
```
### Screenshots
<img width="1075" height="423" alt="image" src="https://github.com/user-attachments/assets/3cfcde3f-dd5a-4f1e-b0e6-dbeda4491b26" />
<img width="952" height="425" alt="image" src="https://github.com/user-attachments/assets/5d93752d-f087-4a47-9d9e-cd7e831b17ec" />

# ☸️ Kubernetes + Helm Deployment
## Start Minikube
```bash
minikube start
```
## Helm Chart Structure
```bash
helm create mern-chart
```

## Helm Values (values.yaml)
```bash
mongodb:
  image: mongo
  port: 27017

backend:
  image: shakti827/mern-backend
  containerPort: 3000
  servicePort: 3000

frontend:
  image: shakti827/mern-frontend
  containerPort: 3000
  servicePort: 3000
  nodePort: 30080

autoscaling:
  enabled: false

```

# Install Helm Chart
```bash
helm install mern-release ./mern-chart
```

### Screenshots
<img width="1512" height="336" alt="image" src="https://github.com/user-attachments/assets/30dcf939-c905-4d2c-8a0f-4932656b17ac" />

---

## After pods are ready:
```bash
kubectl get pods
minikube service frontend

```
### Screenshots
<img width="857" height="142" alt="image" src="https://github.com/user-attachments/assets/72c8d5c9-fc7d-4a66-b1d4-b7158a6f604b" />
<img width="887" height="333" alt="image" src="https://github.com/user-attachments/assets/6525d0e3-bac4-47df-b9d7-78c963779bf1" />

------
