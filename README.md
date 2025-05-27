README.md
# Secure EKS-Style Deployment on Minikube

## Overview
Simulated a secure microservice stack with gateway, auth-service, data-service, and MinIO (mock S3), applying production-grade security policies and observability.

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

Architecture Diagram


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


# Would you like me to:

- Generate the full Helm charts for the three microservices?
- Provide full YAML manifests for MinIO, NetworkPolicy, and Kyverno?
- Prepare the Grafana dashboard JSON template?
- Write the complete README with commands and explanations?
- Help you simulate incidents and show commands to debug?

I can generate each piece step-by-step or package all in a zip-style project structure. What works best for you?