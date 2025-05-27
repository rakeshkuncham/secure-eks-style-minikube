README.md
# Secure EKS-Style Minikube Deployment

## Overview

This repository contains a secure Kubernetes setup using Minikube, simulating a production-like Amazon EKS environment. It includes secure deployment configurations such as role-based access control (RBAC), NetworkPolicies, and HTTPS Ingress with TLS, showcasing strong fundamentals in Kubernetes security and architecture..

## Setup Instructions
1. Start Minikube:
   ```bash
   minikube start --cpus=2 --memory=4096 --addons=ingress,metrics-server
Install Prometheus & Grafana:

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install monitoring prometheus-community/kube-prometheus-stack --namespace monitoring --create-namespace
Deploy microservices with Helm:

helm install gateway ./charts/gateway -n application --create-namespace
helm install auth-service ./charts/auth-service -n application
helm install data-service ./charts/data-service -n application
Deploy MinIO and configure RBAC:


kubectl apply -f charts/minio/minio.yaml -n system
Apply ingress and network policies:


kubectl apply -f ingress/gateway-ingress.yaml -n application
kubectl apply -f networkpolicies/auth-service-egress.yaml -n application
Deploy Kyverno policies for runtime security.




Security Incident
Found auth-service logging Authorization headers — fixed by removing logging in deployment.

Restricted auth-service network egress to only data-service.

Used Kyverno to enforce no logging of Authorization headers.

Observability
Prometheus/Grafana installed for monitoring CPU, memory, pod restarts, and HTTP metrics.

Alert set for pod restarts and failed probes.

Assumptions & Known Issues
MinIO deployed with basic config.

Policies enforce runtime best practices but can be extended.

Gateway exposed via ingress on gateway.local (requires local hosts file edit).


## 🔧 Project Structure

- `manifests/`
  - Deployment YAMLs (frontend, backend, db)
  - ConfigMap, Secret, and Service files
  - NetworkPolicy configuration
  - RBAC roles and bindings
- `ingress/`
  - Ingress setup with TLS
  - Self-signed certificate generation instructions
- `screenshots/`
  - Screenshots for verification (kubectl outputs, app UI, etc.)

---

## ✅ Assessment Checklist

| Task | Status | Description |
|------|--------|-------------|
| Deploy frontend, backend, DB | ✅ Completed | YAML manifests for all |
| Expose frontend via Ingress | ✅ Completed | Configured with TLS (self-signed) |
| Secure database access | ✅ Completed | Access limited only to backend |
| Create restrictive NetworkPolicy | ✅ Completed | Denies all by default, allows only required |
| Use ConfigMap/Secret | ✅ Completed | Frontend uses ConfigMap; backend uses Secret |
| Create Role/RoleBinding | ✅ Completed | RBAC applied to restrict access |
| Screenshots added | ✅ Completed | Proof of successful deployment |

---

## 🛡 Security Features Implemented

- 🔐 **Secrets**: Used for database credentials and stored securely.
- 🗺️ **NetworkPolicy**: Blocks all inter-pod communication except what's explicitly allowed.
- 👮 **RBAC**: Fine-grained access control using Role and RoleBinding.
- 🌐 **Ingress + TLS**: Ingress configured with TLS (self-signed certs).

---

## 📸 Screenshots

All relevant `kubectl` outputs and application screenshots are included under the `screenshots/` folder for verification.

---

## 🚀 How to Run Locally

> Ensure you have Minikube and kubectl installed.

```bash
minikube start
kubectl apply -f manifests/
kubectl apply -f ingress/
Then access the application via the Minikube IP and configured Ingress domain.

🙋‍♂️ Author
Rakesh Kuncham
Level 1 DevOps Engineer
📧 rakeshkuncham777@gmail.com
🌐 GitHub: rakeshkuncham

🏁 Conclusion
This project showcases a secure and production-grade deployment using Minikube with Kubernetes best practices. It simulates real-world scenarios of EKS deployments, ideal for DevOps assessments and practical Kubernetes learning.


### ✅ Next Steps:
1. Go to your GitHub repo → Click `Add file` → `Create new file`
2. Name it `README.md`
3. Paste the above content
4. Commit the new file
