#  Flask App on GKE with Docker & Jenkins

## Build & Push Docker Image to Google Container Registry (GCR)

```bash
gcloud auth configure-docker

docker build -t flask-app .
docker tag flask-app gcr.io/<PROJECT_ID>/flask-app:v1
docker push gcr.io/<PROJECT_ID>/flask-app:v1
```

---

## Create Kubernetes Cluster

```bash
gcloud config set compute/zone europe-west1-c
gcloud container clusters create flask-cluster --num-nodes=4
gcloud container clusters get-credentials flask-cluster
```

---

## Deploy Kubernetes 

```bash
kubectl apply -f deployment.yaml
```

---

## 🌍 8. Expose the App

```bash
kubectl expose deployment flask-deployment \
  --type=LoadBalancer \
  --name=flask-service \
  --port=80 \
  --target-port=8080
```

Check service:
```bash
kubectl get service flask-service
```

---
