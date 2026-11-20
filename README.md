# Flask DevOps CI/CD Application

A lightweight Flask web application demonstrating modern end-to-end DevOps practices, including automated testing, continuous integration, containerization, Kubernetes orchestration, and cloud deployment.

## Features

- **Continuous Integration (CI):** Automated unit testing with `pytest` and GitHub Actions workflow on every push to `main`.
- **Containerization:** Containerized environment using Docker (`python:3.9-slim`) for environment parity and immutability.
- **Orchestration:** Kubernetes Deployment manifests managing multi-replica desired state and NodePort service.
- **Self-Healing Infrastructure:** Kubernetes pod lifecycle and self-healing resilience testing.
- **Continuous Deployment (CD):** Dynamic runtime port binding (`PORT` environment variable) for seamless cloud deployment.

---

## Directory Structure

```plaintext
devops-practical/
├── .github/
│   └── workflows/
│       └── ci.yml               # GitHub Actions CI pipeline
├── k8s/
│   ├── deployment.yaml          # Kubernetes Deployment (2 replicas)
│   └── service.yaml             # Kubernetes NodePort Service
├── app.py                       # Flask application entry point
├── requirements.txt             # Application & test dependencies
├── test_app.py                  # PyTest test suite
├── Dockerfile                   # Docker container specification
└── .gitignore                   # Git ignore patterns
```

---

## Getting Started

### Local Setup & Testing

1. **Create and activate a virtual environment:**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: .\venv\Scripts\activate
   ```

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Run unit tests:**
   ```bash
   pytest
   ```

4. **Run application locally:**
   ```bash
   python app.py
   ```
   Access the app at `http://localhost:5000`.

---

## Docker

1. **Build image:**
   ```bash
   docker build -t flask-app:v1 .
   ```

2. **Run container:**
   ```bash
   docker run -p 5000:5000 flask-app:v1
   ```

3. **Tag & Push to Registry:**
   ```bash
   docker tag flask-app:v1 <your-dockerhub-username>/flask-app:v1
   docker push <your-dockerhub-username>/flask-app:v1
   ```

---

## Kubernetes (Minikube)

1. **Start Minikube:**
   ```bash
   minikube start --driver=docker
   ```

2. **Deploy to cluster:**
   ```bash
   kubectl apply -f k8s/deployment.yaml
   kubectl apply -f k8s/service.yaml
   ```

3. **Verify running pods & access service:**
   ```bash
   kubectl get pods
   minikube service flask-service
   ```
