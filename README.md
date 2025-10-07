# DevOps Assessment - Next.js Containerized Application

[![Build and Push Docker Image](https://github.com/yourusername/nextjs-devops-app/actions/workflows/docker-build-push.yml/badge.svg)](https://github.com/yourusername/nextjs-devops-app/actions/workflows/docker-build-push.yml)

This repository contains a Next.js application containerized with Docker and deployed to Kubernetes using Minikube, demonstrating modern DevOps practices including CI/CD with GitHub Actions.

## 🚀 Project Overview

This project demonstrates:
- **Containerization**: Docker multi-stage build with optimization
- **CI/CD**: Automated build and deployment using GitHub Actions
- **Container Registry**: GitHub Container Registry (GHCR) integration
- **Orchestration**: Kubernetes deployment with health checks
- **Best Practices**: Security, performance, and maintainability

## 📋 Prerequisites

Before you begin, ensure you have the following installed:
- [Node.js](https://nodejs.org/) (v18 or higher)
- [Docker](https://docs.docker.com/get-docker/)
- [Minikube](https://minikube.sigs.k8s.io/docs/start/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [Git](https://git-scm.com/downloads)

## 🛠️ Local Development

### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/nextjs-devops-app.git
cd nextjs-devops-app
```

### 2. Install Dependencies
```bash
npm install
```

### 3. Run Development Server
```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) to view the application.

### 4. Run Linting and Build
```bash
# Linting
npm run lint

# Production build
npm run build

# Start production server
npm start
```

## 🐳 Docker Commands

### Build Docker Image
```bash
docker build -t nextjs-devops-app .
```

### Run Docker Container
```bash
docker run -p 3000:3000 nextjs-devops-app
```

### Build and Tag for GHCR
```bash
docker build -t ghcr.io/yourusername/nextjs-devops-app:latest .
docker push ghcr.io/yourusername/nextjs-devops-app:latest
```

## ☸️ Kubernetes Deployment with Minikube

### 1. Start Minikube
```bash
minikube start
```

### 2. Enable Ingress (Optional)
```bash
minikube addons enable ingress
```

### 3. Deploy to Kubernetes
```bash
# Apply all manifests
kubectl apply -f k8s/

# Or apply individually
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
```

### 4. Check Deployment Status
```bash
# Check pods
kubectl get pods

# Check services
kubectl get services

# Check deployment
kubectl get deployment
```

### 5. Access the Application

#### Option 1: Using NodePort Service
```bash
# Get Minikube IP
minikube ip

# Access application at: http://<minikube-ip>:30080
```

#### Option 2: Using Port Forwarding
```bash
kubectl port-forward service/nextjs-devops-app-service 8080:80

# Access application at: http://localhost:8080
```

#### Option 3: Using Minikube Service
```bash
minikube service nextjs-devops-app-nodeport
```

### 6. Monitor and Debug
```bash
# View logs
kubectl logs -l app=nextjs-devops-app

# Describe pod for troubleshooting
kubectl describe pod <pod-name>

# Execute into pod
kubectl exec -it <pod-name> -- /bin/sh
```

### 7. Clean Up
```bash
# Delete all resources
kubectl delete -f k8s/

# Stop Minikube
minikube stop

# Delete Minikube cluster
minikube delete
```

## 🔄 CI/CD Pipeline

The GitHub Actions workflow (`.github/workflows/docker-build-push.yml`) automatically:

1. **Triggers**: On push to `main` branch or pull requests
2. **Testing**: Runs linting and builds the application
3. **Docker Build**: Creates optimized Docker image
4. **Registry Push**: Pushes to GitHub Container Registry
5. **Tagging**: Uses semantic versioning and branch-based tags

### GitHub Actions Features:
- ✅ Automated testing and linting
- ✅ Multi-stage Docker builds with caching
- ✅ Secure GHCR authentication
- ✅ Proper image tagging strategy
- ✅ Build optimization with GitHub Actions cache

## 📁 Project Structure

```
nextjs-devops-app/
├── .github/
│   └── workflows/
│       └── docker-build-push.yml    # GitHub Actions CI/CD
├── k8s/
│   ├── deployment.yaml              # Kubernetes deployment
│   └── service.yaml                 # Kubernetes service
├── public/                          # Static assets
├── src/
│   └── app/                         # Next.js app directory
├── .dockerignore                    # Docker ignore file
├── .gitignore                      # Git ignore file
├── Dockerfile                      # Multi-stage Docker build
├── next.config.ts                  # Next.js configuration
├── package.json                    # Node.js dependencies
└── README.md                       # This file
```

## 🔧 Configuration Details

### Dockerfile Optimizations
- **Multi-stage build**: Reduces final image size
- **Alpine Linux**: Lightweight base image
- **Non-root user**: Enhanced security
- **Standalone output**: Optimized for containerization
- **Layer caching**: Efficient rebuilds

### Kubernetes Configuration
- **Replicas**: 3 instances for high availability
- **Health checks**: Readiness and liveness probes
- **Resource limits**: CPU and memory constraints
- **Service types**: LoadBalancer and NodePort options
- **Labels**: Proper resource organization

### Security Best Practices
- Non-root container execution
- Minimal base image (Alpine)
- Read-only root filesystem capability
- Resource limits and requests
- Health check endpoints

## 🌐 Accessing the Deployed Application

After successful deployment, you can access the application through:

1. **Minikube Service**: `minikube service nextjs-devops-app-nodeport`
2. **NodePort**: `http://<minikube-ip>:30080`
3. **Port Forward**: `kubectl port-forward service/nextjs-devops-app-service 8080:80`

## 🐛 Troubleshooting

### Common Issues

1. **Pod not starting**: Check resource constraints and image availability
2. **Service not accessible**: Verify service and endpoint configuration
3. **Build failures**: Check Docker daemon and permissions
4. **GHCR push issues**: Verify GitHub token permissions

### Debug Commands
```bash
# Check pod events
kubectl describe pod <pod-name>

# View container logs
kubectl logs <pod-name> -c nextjs-devops-app

# Check service endpoints
kubectl get endpoints

# Verify Docker image
docker pull ghcr.io/yourusername/nextjs-devops-app:latest
```

## 📝 Environment Variables

| Variable | Description | Default |
|----------|-------------|----------|
| `NODE_ENV` | Node.js environment | `production` |
| `PORT` | Application port | `3000` |
| `HOSTNAME` | Bind hostname | `0.0.0.0` |

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🎯 Assessment Completion

This project fulfills all assessment requirements:

- ✅ **Next.js Application**: Created with TypeScript and Tailwind CSS
- ✅ **Dockerfile**: Multi-stage build with optimization
- ✅ **GitHub Actions**: Automated CI/CD pipeline
- ✅ **GHCR Integration**: Container registry push
- ✅ **Kubernetes Manifests**: Deployment and service configuration
- ✅ **Documentation**: Comprehensive setup and deployment guide
- ✅ **Best Practices**: Security, performance, and maintainability

---

**DevOps Assessment Submission by Bharath Kumar**

📧 Repository: `https://github.com/yourusername/nextjs-devops-app`  
🐳 GHCR Image: `ghcr.io/yourusername/nextjs-devops-app:latest`
