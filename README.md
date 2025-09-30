# Kubernetes WeCloudData Labs

[![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat&logo=kubernetes&logoColor=white)](https://kubernetes.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A comprehensive Kubernetes learning project designed for WeCloudData DevOps training labs. This repository contains practical examples of various Kubernetes resources and concepts, including Deployments, ReplicaSets, Pods, Services, ConfigMaps, and Secrets.

## 📋 Table of Contents

- [Overview](#overview)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Kubernetes Resources](#kubernetes-resources)
- [Usage Examples](#usage-examples)
- [Learning Objectives](#learning-objectives)
- [Contributing](#contributing)
- [Authors](#authors)
- [License](#license)

## 🎯 Overview

This project serves as a hands-on learning environment for Kubernetes administration and DevOps practices. It demonstrates core Kubernetes concepts through practical examples, allowing students to deploy, manage, and understand containerized applications in a Kubernetes cluster.

**Key Features:**
- Namespace isolation and resource organization
- Multiple deployment strategies (Deployments, ReplicaSets, Pods)
- Service networking and exposure
- Configuration management with ConfigMaps
- Secret management for sensitive data
- Resource limits and requests configuration
- Rolling update strategies

## 📁 Project Structure

```
k8s-weclouddata-labs/
├── namespace.yml      # Creates 'weclouddata' namespace
├── deployment.yml     # Nginx deployment with 3 replicas and rolling updates
├── replicaset.yml     # ReplicaSet example for managing pod replicas
├── pod.yml            # Standalone nginx pod configuration
├── pod5.yml           # Busybox pod with ConfigMap and Secret injection
├── services.yml       # ClusterIP service exposing nginx
├── configmaps.yml     # Configuration data storage
├── secrets.yml        # Base64-encoded sensitive data
└── README.md          # This file
```

## 🔧 Prerequisites

Before you begin, ensure you have the following installed:

- **Docker Desktop** (with Kubernetes enabled) OR **Minikube**
  - [Docker Desktop Installation](https://www.docker.com/products/docker-desktop)
  - [Minikube Installation](https://minikube.sigs.k8s.io/docs/start/)
- **kubectl** - Kubernetes command-line tool
  - [kubectl Installation](https://kubernetes.io/docs/tasks/tools/)
- **Git** - Version control system

Verify your setup:
```bash
kubectl version --client
kubectl cluster-info
```

## 🚀 Installation

Follow these steps to set up and deploy the project:

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/k8s-weclouddata-labs.git
cd k8s-weclouddata-labs
```

### 2. Deploy Resources (Recommended Order)

**Important:** Apply resources in the following order to avoid dependency issues:

```bash
# Step 1: Create the namespace
kubectl apply -f namespace.yml

# Step 2: Create ConfigMaps and Secrets
kubectl apply -f configmaps.yml
kubectl apply -f secrets.yml

# Step 3: Deploy the application resources
kubectl apply -f deployment.yml
kubectl apply -f replicaset.yml
kubectl apply -f services.yml

# Step 4: Create standalone pods
kubectl apply -f pod.yml
kubectl apply -f pod5.yml
```

### 3. Verify Deployment

```bash
# Check all resources in the weclouddata namespace
kubectl get all -n weclouddata

# Check ConfigMaps and Secrets
kubectl get configmaps,secrets -n weclouddata
```

## 📦 Kubernetes Resources

### Namespace (`namespace.yml`)
Creates an isolated environment named `weclouddata` for all resources.

### Deployment (`deployment.yml`)
- **Application:** Nginx web server (using httpd:latest image)
- **Replicas:** 3 pods
- **Strategy:** RollingUpdate (maxUnavailable: 1, maxSurge: 1)
- **Resources:** CPU (100m-250m), Memory (128Mi-256Mi)
- **Purpose:** Demonstrates production-grade deployment with high availability

### ReplicaSet (`replicaset.yml`)
- **Application:** Nginx (nginx:latest)
- **Replicas:** 3 pods
- **Purpose:** Shows how ReplicaSets maintain desired pod count
- **Note:** Deployments are preferred in production as they manage ReplicaSets automatically

### Service (`services.yml`)
- **Type:** ClusterIP
- **Port:** 80
- **Purpose:** Provides internal load balancing and service discovery for nginx pods

### ConfigMap (`configmaps.yml`)
Stores non-sensitive configuration data:
- `Program`: DevOps
- `Instructor`: Usman

### Secret (`secrets.yml`)
Stores base64-encoded sensitive data:
- `username`: wcd (d2Nk)
- `password`: thisismypassword (dGhpc2lzbXlwYXNzd29yZA==)

### Pods
- **pod.yml:** Standalone nginx pod with resource limits
- **pod5.yml:** Busybox container demonstrating:
  - ConfigMap injection as environment variables
  - Secret injection as environment variables
  - Long-running container (sleep 3600)

## 💡 Usage Examples

### Access the Nginx Service

```bash
# Port-forward to access the service locally
kubectl port-forward -n weclouddata service/nginx-service 8080:80

# Visit http://localhost:8080 in your browser
```

### View ConfigMap and Secret Values in Pod

```bash
# Execute into the busybox pod
kubectl exec -it -n weclouddata mybox -- sh

# Inside the pod, view environment variables
echo $Program      # Output: DevOps
echo $Instructor   # Output: Usman
echo $username     # Output: wcd
echo $password     # Output: thisismypassword
exit
```

### Monitor Deployment Rollout

```bash
# Watch deployment status
kubectl rollout status -n weclouddata deployment/nginx-deployment

# View deployment history
kubectl rollout history -n weclouddata deployment/nginx-deployment
```

### Scale the Deployment

```bash
# Scale to 5 replicas
kubectl scale deployment/nginx-deployment -n weclouddata --replicas=5

# Verify scaling
kubectl get pods -n weclouddata -l app=nginx
```

### Clean Up Resources

```bash
# Delete all resources in the namespace
kubectl delete -f .

# Or delete the entire namespace
kubectl delete namespace weclouddata
```

## 🎓 Learning Objectives

This project helps you understand:

1. **Namespace Management:** Resource isolation and organization
2. **Workload Management:** Deployments vs ReplicaSets vs Pods
3. **Service Networking:** Internal load balancing and service discovery
4. **Configuration Management:** Separating config from code using ConfigMaps
5. **Secret Management:** Securely handling sensitive data
6. **Resource Management:** Setting CPU and memory limits/requests
7. **Deployment Strategies:** Rolling updates with zero downtime
8. **Environment Variables:** Injecting configuration into containers

## 🤝 Contributing

Contributions are welcome! This is a public educational project, and everyone is encouraged to contribute.

### How to Contribute:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Contribution Ideas:
- Add more Kubernetes resource examples (StatefulSets, DaemonSets, Jobs)
- Improve documentation and tutorials
- Add Helm charts
- Create CI/CD pipeline examples
- Add monitoring and logging configurations

## 👨‍💻 Authors

* **Juan Mosquera** - *Initial work and project creator*

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

**Happy Learning! 🚀**

For questions or issues, please open an issue in the repository or contact the WeCloudData DevOps team.
