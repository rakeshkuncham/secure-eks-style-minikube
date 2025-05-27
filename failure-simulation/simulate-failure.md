# Failure Simulations for Secure EKS-style Minikube

This document outlines various failure simulations to test the resilience of your Kubernetes environment.

---

## 1. **Pod Crash Simulation**
### Scenario
Force a crash in a deployment pod to test auto-restart.
### Command
```bash
kubectl delete pod -l app=auth-service
