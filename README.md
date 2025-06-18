# ArgoCD Multi-Environment Setup

This repository contains the GitOps configuration for managing multiple applications across different environments (dev, QA, prod) using ArgoCD.

## Repository Structure

```
.
├── apps/                    # Application configurations
│   ├── dev/                # Development environment
│   ├── qa/                 # QA environment
│   └── prod/               # Production environment
└── k8s/                    # Kubernetes configurations
    └── argocd/            # ArgoCD specific configurations
```

## Setup Instructions

1. Start Minikube:
   ```bash
   minikube start
   ```

2. Install ArgoCD:
   ```bash
   kubectl create namespace argocd
   kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
   ```

3. Access ArgoCD:
   ```bash
   kubectl port-forward svc/argocd-server -n argocd 8080:443
   ```
   Then visit: https://localhost:8080

4. Get initial admin password:
   ```bash
   kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
   ```

## Adding New Applications

To add a new application:
1. Create application manifests in the respective environment directory under `apps/`
2. Create an Application CR in the corresponding environment directory
3. Commit and push changes to trigger automatic deployment

## Environment-Specific Configurations

Each environment (dev, qa, prod) has its own directory with specific configurations:
- `apps/dev/`: Development environment configurations
- `apps/qa/`: QA environment configurations
- `apps/prod/`: Production environment configurations # argoworkflow
