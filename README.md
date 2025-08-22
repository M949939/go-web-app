# Full Deployment Documentation – Go Web App (Zahed)

This document describes **all the steps performed** to deploy the Go Web App using Docker, Kubernetes, Helm, ArgoCD, and AWS EKS.  
It includes repository setup, cluster setup, manifests, Helm, Ingress, ArgoCD, debugging, and verification.

---

## 1. Repository Setup

- Clone the original repository:

```bash
git clone https://github.com/iam-veeramalla/go-web-app.git
cd go-web-app/
```

- Configure Git remotes and branches:

```bash
git remote add origin https://github.com/M949939/go-web-app.git
```

---

## 2. AWS CLI Setup

- Install AWS CLI v2:

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
aws --version
```

- Configure AWS credentials:

```bash
aws configure
```

---

## 3. EKS Cluster Setup

- Install eksctl:

```bash
ARCH=amd64
PLATFORM=$(uname -s)_$ARCH
curl -sLO "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$PLATFORM.tar.gz"
tar -xzf eksctl_$PLATFORM.tar.gz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
eksctl version
```

- Create EKS cluster:

```bash
eksctl create cluster --name go-web-cluster --region eu-west-3 --nodes 2 --node-type t3.medium
```

---

## 4. Helm Setup

- Install Helm:

```bash
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
helm version
```

- Create Helm chart for app:

```bash
helm create go-web-app
```

---

## 5. Kubernetes Manifests

- Deployment (`deployment.yaml`)
- Service (`service.yaml`)
- Ingress (`ingress.yaml`)
---

## 6. ArgoCD AppProject
- appProject (`appProject.yaml`)
- application (`application.yaml`) (inside ArgoCD)
---

## 7. Debugging and Verification

- Describe ingress:

```bash
kubectl describe ingress go-web-app
```

- Verify from inside cluster:

```bash
kubectl exec -it deploy/go-web-app -- wget -qO- http://localhost:8080/courses
```

- Verify externally with host header:

```bash
curl -H "Host: go-web-app.local" http://<AWS-ELB-ADDRESS>/courses
```

---

✅ At this point, the Go Web App is deployed on EKS, accessible through NGINX Ingress with Helm, and managed by ArgoCD.
---
Credit: https://github.com/iam-veeramalla/go-web-app-devops

