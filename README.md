# Kubernetes WeCloudData Labs

[![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat&logo=kubernetes&logoColor=white)](https://kubernetes.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)
[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)](https://github.com/yourusername/k8s-weclouddata-labs/graphs/commit-activity)

> **A hands-on Kubernetes learning laboratory** - Master container orchestration through practical, real-world examples! 🚀

A comprehensive Kubernetes learning project designed for WeCloudData DevOps training labs. This repository contains practical examples of various Kubernetes resources and concepts, including Deployments, ReplicaSets, Pods, Services, ConfigMaps, and Secrets. Perfect for beginners and intermediate learners looking to gain practical Kubernetes experience.

## 📋 Table of Contents

- [Quick Start](#-quick-start)
- [Overview](#overview)
- [Architecture](#-architecture)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Kubernetes Resources](#kubernetes-resources)
- [Usage Examples](#usage-examples)
- [Best Practices](#-best-practices)
- [Troubleshooting](#-troubleshooting)
- [FAQ](#-faq)
- [Learning Objectives](#learning-objectives)
- [Resources & Further Reading](#-resources--further-reading)
- [Contributing](#contributing)
- [Authors](#authors)
- [License](#license)

## ⚡ Quick Start

Get up and running in under 5 minutes!

```bash
# 1. Clone the repository
git clone https://github.com/yourusername/k8s-weclouddata-labs.git
cd k8s-weclouddata-labs

# 2. Verify Kubernetes is running
kubectl cluster-info

# 3. Deploy all resources in one command
kubectl apply -f namespace.yml && \
kubectl apply -f configmaps.yml && \
kubectl apply -f secrets.yml && \
kubectl apply -f deployment.yml && \
kubectl apply -f replicaset.yml && \
kubectl apply -f services.yml && \
kubectl apply -f pod.yml && \
kubectl apply -f pod5.yml

# 4. Verify deployment
kubectl get all -n weclouddata

# 5. Access the application
kubectl port-forward -n weclouddata service/nginx-service 8080:80
# Visit http://localhost:8080 in your browser
```

**Expected Output:**
```
NAME                                    READY   STATUS    RESTARTS   AGE
pod/mybox                               1/1     Running   0          30s
pod/nginx-deployment-xxxxxxxxxx-xxxxx   1/1     Running   0          30s
pod/nginx-deployment-xxxxxxxxxx-xxxxx   1/1     Running   0          30s
pod/nginx-deployment-xxxxxxxxxx-xxxxx   1/1     Running   0          30s
pod/nginx-pod                           1/1     Running   0          30s
...
```

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

## 🏗️ Architecture

This project demonstrates a typical Kubernetes application architecture with multiple layers:

```
┌─────────────────────────────────────────────────────────────┐
│                     Kubernetes Cluster                       │
│                                                               │
│  ┌────────────────────────────────────────────────────────┐ │
│  │         Namespace: weclouddata                         │ │
│  │                                                          │ │
│  │  ┌──────────────────────────────────────────────────┐  │ │
│  │  │  Service Layer (ClusterIP)                       │  │ │
│  │  │  nginx-service (Port 80)                         │  │ │
│  │  └─────────────┬────────────────────────────────────┘  │ │
│  │                │ Load Balancing                         │ │
│  │  ┌─────────────▼────────────────────────────────────┐  │ │
│  │  │  Deployment: nginx-deployment (3 replicas)       │  │ │
│  │  │  ┌─────────┐  ┌─────────┐  ┌─────────┐          │  │ │
│  │  │  │  Pod 1  │  │  Pod 2  │  │  Pod 3  │          │  │ │
│  │  │  │ (httpd) │  │ (httpd) │  │ (httpd) │          │  │ │
│  │  │  └─────────┘  └─────────┘  └─────────┘          │  │ │
│  │  └──────────────────────────────────────────────────┘  │ │
│  │                                                          │ │
│  │  ┌──────────────────────────────────────────────────┐  │ │
│  │  │  ReplicaSet: nginx-rs (3 replicas)              │  │ │
│  │  └──────────────────────────────────────────────────┘  │ │
│  │                                                          │ │
│  │  ┌──────────────────────────────────────────────────┐  │ │
│  │  │  Standalone Pods                                 │  │ │
│  │  │  • nginx-pod (nginx)                             │  │ │
│  │  │  • mybox (busybox with env vars)                │  │ │
│  │  └──────────────────────────────────────────────────┘  │ │
│  │                                                          │ │
│  │  ┌──────────────────────────────────────────────────┐  │ │
│  │  │  Configuration Layer                             │  │ │
│  │  │  • ConfigMap (non-sensitive config)             │  │ │
│  │  │  • Secret (sensitive data)                       │  │ │
│  │  └──────────────────────────────────────────────────┘  │ │
│  └────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

**Component Interactions:**
- **Service** acts as a load balancer distributing traffic to deployment pods
- **Deployment** manages ReplicaSets and ensures desired state
- **ConfigMaps & Secrets** inject configuration into pods as environment variables
- **Resource quotas** prevent resource exhaustion

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

### System Requirements

**Minimum Hardware:**
- **CPU:** 2 cores
- **RAM:** 4 GB
- **Disk Space:** 20 GB free

**Recommended Hardware:**
- **CPU:** 4 cores or more
- **RAM:** 8 GB or more
- **Disk Space:** 50 GB free

### Required Software

Before you begin, ensure you have the following installed:

- **Docker Desktop** (with Kubernetes enabled) OR **Minikube**
  - [Docker Desktop Installation](https://www.docker.com/products/docker-desktop)
  - [Minikube Installation](https://minikube.sigs.k8s.io/docs/start/)
  - *Note:* Ensure Kubernetes is enabled in Docker Desktop settings
- **kubectl** - Kubernetes command-line tool (v1.20+)
  - [kubectl Installation](https://kubernetes.io/docs/tasks/tools/)
- **Git** - Version control system
  - [Git Installation](https://git-scm.com/downloads)

### Verify Your Setup

Run these commands to ensure everything is properly configured:

```bash
# Check kubectl version (should be v1.20 or higher)
kubectl version --client

# Verify cluster connectivity
kubectl cluster-info

# Check available nodes
kubectl get nodes

# Verify you can create resources
kubectl auth can-i create deployments --all-namespaces
```

**Expected Output:**
```
Client Version: v1.28.0
Kustomize Version: v5.0.4-0.20230601165947-6ce0bf390ce3
Kubernetes control plane is running at https://127.0.0.1:6443
...
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

**Expected Output:**
```
Forwarding from 127.0.0.1:8080 -> 80
Forwarding from [::1]:8080 -> 80
Handling connection for 8080
```

You should see the default Apache/Nginx welcome page in your browser.

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

**Expected Output:**
```
DevOps
Usman
wcd
thisismypassword
```

This demonstrates how ConfigMaps and Secrets are successfully injected as environment variables.

### Monitor Deployment Rollout

```bash
# Watch deployment status
kubectl rollout status -n weclouddata deployment/nginx-deployment

# View deployment history
kubectl rollout history -n weclouddata deployment/nginx-deployment
```

**Expected Output:**
```
deployment "nginx-deployment" successfully rolled out

REVISION  CHANGE-CAUSE
1         <none>
```

### Scale the Deployment

```bash
# Scale to 5 replicas
kubectl scale deployment/nginx-deployment -n weclouddata --replicas=5

# Verify scaling
kubectl get pods -n weclouddata -l app=nginx
```

**Expected Output:**
```
deployment.apps/nginx-deployment scaled

NAME                                READY   STATUS    RESTARTS   AGE
nginx-deployment-xxxxxxxxxx-xxxxx   1/1     Running   0          2m
nginx-deployment-xxxxxxxxxx-xxxxx   1/1     Running   0          2m
nginx-deployment-xxxxxxxxxx-xxxxx   1/1     Running   0          2m
nginx-deployment-xxxxxxxxxx-xxxxx   1/1     Running   0          10s
nginx-deployment-xxxxxxxxxx-xxxxx   1/1     Running   0          10s
```

### Clean Up Resources

```bash
# Delete all resources in the namespace
kubectl delete -f .

# Or delete the entire namespace
kubectl delete namespace weclouddata
```

## 📚 Best Practices

### Resource Management
- **Always set resource limits and requests** to prevent resource exhaustion
- **Use namespaces** to isolate different environments (dev, staging, prod)
- **Implement health checks** with liveness and readiness probes
- **Use horizontal pod autoscaling (HPA)** for automatic scaling based on load

### Security
- **Never commit secrets to Git** - use encrypted secret management tools
- **Use RBAC (Role-Based Access Control)** to limit access to resources
- **Run containers as non-root users** when possible
- **Regularly update container images** to patch security vulnerabilities
- **Use network policies** to restrict pod-to-pod communication

### Configuration Management
- **Separate configuration from code** using ConfigMaps and Secrets
- **Use version control** for all Kubernetes manifests
- **Apply labels and annotations** for better resource organization and tracking
- **Document environment variables** and their purposes

### Deployment Strategies
- **Use Deployments over ReplicaSets** for better management and rollback capabilities
- **Implement rolling updates** to ensure zero-downtime deployments
- **Test in lower environments** before deploying to production
- **Keep replica counts odd** (3, 5, 7) for better quorum in distributed systems
- **Use readiness probes** to ensure traffic only goes to ready pods

### Monitoring and Logging
- **Implement centralized logging** to aggregate logs from all pods
- **Set up monitoring and alerting** for resource usage and application health
- **Use kubectl describe and logs** for troubleshooting issues
- **Monitor pod resource usage** to optimize resource requests/limits

### Example: Production-Ready Deployment Pattern
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app-deployment
  labels:
    app: myapp
    version: v1.0.0
    environment: production
spec:
  replicas: 3
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 0
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
        version: v1.0.0
    spec:
      containers:
      - name: app
        image: myapp:1.0.0
        resources:
          requests:
            memory: "128Mi"
            cpu: "100m"
          limits:
            memory: "256Mi"
            cpu: "200m"
        livenessProbe:
          httpGet:
            path: /health
            port: 8080
          initialDelaySeconds: 30
          periodSeconds: 10
        readinessProbe:
          httpGet:
            path: /ready
            port: 8080
          initialDelaySeconds: 5
          periodSeconds: 5
```

## 🔧 Troubleshooting

### Common Issues and Solutions

#### 1. Pods Not Starting (ImagePullBackOff)
**Symptom:** Pods stuck in `ImagePullBackOff` or `ErrImagePull` state

**Solution:**
```bash
# Check pod events
kubectl describe pod <pod-name> -n weclouddata

# Verify image exists and is accessible
docker pull httpd:latest
docker pull nginx:latest
```

**Common Causes:**
- Image name typo in YAML file
- Network connectivity issues
- Private registry authentication required

#### 2. Service Not Accessible
**Symptom:** Cannot access service via port-forward or ClusterIP

**Solution:**
```bash
# Verify service exists and has endpoints
kubectl get svc -n weclouddata
kubectl get endpoints -n weclouddata

# Check if pods are running and ready
kubectl get pods -n weclouddata -l app=nginx

# Verify service selector matches pod labels
kubectl describe svc nginx-service -n weclouddata
```

#### 3. Namespace Already Exists Error
**Symptom:** `Error from server (AlreadyExists): namespaces "weclouddata" already exists`

**Solution:**
```bash
# This is normal if namespace already exists - you can safely ignore
# Or delete and recreate:
kubectl delete namespace weclouddata
kubectl apply -f namespace.yml
```

#### 4. Resource Quota Exceeded
**Symptom:** Pods stuck in `Pending` state

**Solution:**
```bash
# Check pod status and events
kubectl describe pod <pod-name> -n weclouddata

# Check resource availability
kubectl top nodes
kubectl describe nodes

# Reduce replica count or resource requests if needed
kubectl scale deployment/nginx-deployment -n weclouddata --replicas=1
```

#### 5. ConfigMap/Secret Not Found
**Symptom:** Pods crash with "ConfigMap not found" or "Secret not found"

**Solution:**
```bash
# Ensure ConfigMaps and Secrets are created first
kubectl apply -f configmaps.yml
kubectl apply -f secrets.yml

# Verify they exist
kubectl get configmaps,secrets -n weclouddata

# Then create the pods
kubectl apply -f pod5.yml
```

#### 6. Permission Denied Errors
**Symptom:** `Error from server (Forbidden): ... is forbidden`

**Solution:**
```bash
# Check your permissions
kubectl auth can-i create deployments --all-namespaces

# If using Minikube, ensure you're using the correct context
kubectl config current-context
kubectl config use-context minikube
```

#### 7. Port Already in Use
**Symptom:** `bind: address already in use` when using port-forward

**Solution:**
```bash
# Use a different local port
kubectl port-forward -n weclouddata service/nginx-service 8081:80

# Or find and kill the process using port 8080
# Windows:
netstat -ano | findstr :8080
taskkill /PID <PID> /F

# Linux/Mac:
lsof -ti:8080 | xargs kill -9
```

### Debug Commands Cheat Sheet

```bash
# Get detailed information about a resource
kubectl describe <resource-type> <resource-name> -n weclouddata

# View pod logs
kubectl logs <pod-name> -n weclouddata
kubectl logs <pod-name> -n weclouddata --previous  # Previous container logs

# Execute commands inside a pod
kubectl exec -it <pod-name> -n weclouddata -- sh

# Get events in the namespace
kubectl get events -n weclouddata --sort-by='.lastTimestamp'

# Check resource usage
kubectl top pods -n weclouddata
kubectl top nodes

# View YAML configuration of running resource
kubectl get deployment nginx-deployment -n weclouddata -o yaml
```

## ❓ FAQ

### General Questions

**Q: What's the difference between a Deployment, ReplicaSet, and Pod?**
A: 
- **Pod:** The smallest deployable unit in Kubernetes, representing one or more containers
- **ReplicaSet:** Ensures a specified number of pod replicas are running at any time
- **Deployment:** Higher-level abstraction that manages ReplicaSets and provides declarative updates, rollbacks, and scaling

**Q: Why use Deployments instead of ReplicaSets directly?**
A: Deployments provide additional features like rolling updates, rollback capabilities, and declarative updates. They automatically manage ReplicaSets for you, making them the recommended approach for stateless applications.

**Q: When should I use ConfigMaps vs Secrets?**
A: 
- **ConfigMaps:** For non-sensitive configuration data (URLs, feature flags, configuration files)
- **Secrets:** For sensitive data (passwords, API keys, certificates). Secrets are base64-encoded and can be encrypted at rest.

**Q: What's the purpose of the namespace in this project?**
A: Namespaces provide logical isolation for resources, allowing multiple teams or projects to share a cluster without interfering with each other. The `weclouddata` namespace isolates all resources for this lab.

### Technical Questions

**Q: Why do some pods use httpd while others use nginx?**
A: This is intentional for learning purposes. The deployment uses `httpd:latest` to demonstrate that you can use different web server images. The ReplicaSet and standalone pods use `nginx:latest` to show variety.

**Q: How do I access the service from outside the cluster?**
A: By default, ClusterIP services are only accessible within the cluster. Options for external access:
1. Use `kubectl port-forward` (for testing)
2. Change service type to `NodePort` or `LoadBalancer`
3. Set up an Ingress controller

**Q: Are the secrets actually secure with base64 encoding?**
A: **No!** Base64 is encoding, not encryption. In production:
- Enable encryption at rest in etcd
- Use external secret management tools (HashiCorp Vault, AWS Secrets Manager)
- Implement RBAC to restrict access
- Never commit secrets to version control

**Q: Can I use this in production?**
A: This project is designed for learning and development. For production:
- Add health checks (liveness and readiness probes)
- Implement proper logging and monitoring
- Use encrypted secrets management
- Set up proper resource quotas and limits
- Implement network policies
- Use CI/CD pipelines for deployment

**Q: How do I update the application to a new version?**
A:
```bash
# Update the image in deployment.yml, then:
kubectl apply -f deployment.yml

# Or use kubectl set image:
kubectl set image deployment/nginx-deployment nginx=httpd:2.4 -n weclouddata

# Monitor the rollout:
kubectl rollout status deployment/nginx-deployment -n weclouddata

# Rollback if needed:
kubectl rollout undo deployment/nginx-deployment -n weclouddata
```

**Q: What happens if I delete a pod from a Deployment?**
A: Kubernetes will automatically create a new pod to maintain the desired replica count. This is called self-healing.

```bash
# Try it:
kubectl delete pod <pod-name> -n weclouddata
kubectl get pods -n weclouddata  # You'll see a new pod created
```

**Q: How much does this cost to run?**
A: If you're using Docker Desktop or Minikube on your local machine, it's completely free! Cloud-based Kubernetes services (EKS, GKE, AKS) would incur costs.

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

## 📖 Resources & Further Reading

### Official Documentation
- [Kubernetes Official Documentation](https://kubernetes.io/docs/home/)
- [Kubectl Command Reference](https://kubernetes.io/docs/reference/kubectl/)
- [Kubernetes API Reference](https://kubernetes.io/docs/reference/kubernetes-api/)
- [Kubernetes Best Practices](https://kubernetes.io/docs/concepts/configuration/overview/)

### Interactive Learning
- [Kubernetes Official Tutorial](https://kubernetes.io/docs/tutorials/kubernetes-basics/)
- [Play with Kubernetes](https://labs.play-with-k8s.com/) - Free browser-based Kubernetes playground
- [Katacoda Kubernetes Scenarios](https://www.katacoda.com/courses/kubernetes) - Interactive learning scenarios
- [KillerCoda](https://killercoda.com/kubernetes) - Hands-on Kubernetes scenarios

### Books & Courses
- **Books:**
  - "Kubernetes in Action" by Marko Lukša
  - "Kubernetes: Up and Running" by Kelsey Hightower
  - "The Kubernetes Book" by Nigel Poulton
- **Free Courses:**
  - [Introduction to Kubernetes (edX)](https://www.edx.org/course/introduction-to-kubernetes)
  - [Kubernetes for Beginners (YouTube)](https://www.youtube.com/watch?v=X48VuDVv0do)

### Tools & Extensions
- [K9s](https://k9scli.io/) - Terminal-based UI for managing Kubernetes clusters
- [Lens](https://k8slens.dev/) - Kubernetes IDE
- [Helm](https://helm.sh/) - Kubernetes package manager
- [Kustomize](https://kustomize.io/) - Kubernetes native configuration management
- [kubectx & kubens](https://github.com/ahmetb/kubectx) - Fast context and namespace switching

### Community & Support
- [Kubernetes Slack](https://slack.k8s.io/) - Official Kubernetes Slack workspace
- [Kubernetes Forum](https://discuss.kubernetes.io/) - Community discussion forum
- [Stack Overflow - Kubernetes Tag](https://stackoverflow.com/questions/tagged/kubernetes)
- [Reddit r/kubernetes](https://www.reddit.com/r/kubernetes/)

### WeCloudData Resources
- [WeCloudData Official Website](https://weclouddata.com/)
- WeCloudData DevOps Program Materials
- Internal Learning Portal

### Cheat Sheets
- [Official Kubernetes Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
- [Kubernetes Quick Reference](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands)

### Advanced Topics
- **Service Mesh:** Istio, Linkerd
- **CI/CD:** ArgoCD, Flux, Jenkins X
- **Monitoring:** Prometheus, Grafana
- **Logging:** ELK Stack, Fluentd
- **Security:** OPA (Open Policy Agent), Falco
- **Storage:** Persistent Volumes, StatefulSets

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
