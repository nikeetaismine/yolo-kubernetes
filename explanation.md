# Explanation of Architecture and Design Choices

## 🎯 Objective

The goal was to containerize and deploy a full-stack e-commerce application using Kubernetes on **Google Kubernetes Engine (GKE)**, while avoiding the use of Ingress or domain names.

---

## ⚙️ Kubernetes Components

### 1. **MongoDB (StatefulSet)**
- Deployed using `StatefulSet` to maintain stable network identity.
- Headless service used for stable DNS within the cluster.
- Init container in backend waits for MongoDB to be ready before starting.

### 2. **Backend Service (Node.js)**
- Exposes port `5000` internally.
- Exposed to the outside using a `NodePort` on port `30001`.
- Connects to MongoDB via DNS: `mongo-0.mongo:27017`.

### 3. **Frontend Service (React)**
- Runs on port `3000`, exposed via a `LoadBalancer` service.
- Uses an environment variable `REACT_APP_BACKEND_URL` to communicate with the backend's external IP and NodePort.

---

## 🔀 Communication Flow

Browser → Frontend LoadBalancer → React App → Backend NodePort → Backend Service → MongoDB StatefulSet

---

## ✅ Summary

This deployment:

- Uses best practices for MongoDB in Kubernetes.
- Connects frontend to backend using `REACT_APP_BACKEND_URL`.
- Successfully exposes the app externally via GKE LoadBalancer IP.
