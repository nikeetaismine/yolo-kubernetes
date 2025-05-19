# YOLO E-Commerce App - Kubernetes Deployment

This project is a simple e-commerce application called YOLO, deployed on **Google Kubernetes Engine (GKE)** using:

- **Frontend**: React
- **Backend**: Node.js (Express)
- **Database**: MongoDB (StatefulSet)

The frontend and backend Docker images are hosted on Docker Hub.

## ✅ Project Structure

yolo-kubernetes/
├── manifests/
│ ├── mongo-statefulset.yaml
│ ├── backend-deployment.yaml
│ ├── frontend-deployment.yaml


## 🚀 Deployment Instructions

1. **Clone this repository**:
   ```bash
   git clone <your-repo-url>
   cd yolo-kubernetes/manifests

2. **Ensure Docker images are available:**

    Frontend: denisemwangi/yolo-client:v1.0.1

    Backend: denisemwangi/yolo-backend:v1.0.0

3. **Deploy to GKE:**

    kubectl apply -f mongo-statefulset.yaml
    kubectl apply -f backend-deployment.yaml
    kubectl apply -f frontend-deployment.yaml

4. **Wait for External IP:**

    kubectl get svc frontend-service

In this case: 

    NAME               TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
    frontend-service   LoadBalancer   34.118.229.137   34.59.122.3   80:31557/TCP     34h

5. **Access the Application:**

    Open a browser and navigate to:
        http://34.59.122.3