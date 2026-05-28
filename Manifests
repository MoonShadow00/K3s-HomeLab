manifests/README.md
# Kubernetes Manifests

## Overview

This repository contains raw Kubernetes manifests used throughout the Kubernetes HomeLab environment.

The manifests are used to deploy, configure, and manage:

- Applications
- Services
- Deployments
- Namespaces
- ConfigMaps
- Secrets
- Ingress resources
- Persistent storage
- Networking components

---

# Purpose

This repository exists to:

- Learn Kubernetes resource management
- Practice infrastructure deployment
- Maintain reusable manifests
- Version control Kubernetes configurations
- Build production-aligned deployment workflows

---

# Repository Structure

```text

.
├── apps/
├── networking/
├── storage/
├── ingress/
├── monitoring/
├── security/
├── namespaces/
└── README.md
________________________________________
Example Deployment

apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx:latest
          ports:
            - containerPort: 80
________________________________________
Common Commands
Apply Manifest

kubectl apply -f deployment.yaml
Delete Manifest

kubectl delete -f deployment.yaml
Validate Resources

kubectl get all -A
________________________________________
Learning Areas
•	Kubernetes resource management
•	YAML configuration
•	Infrastructure deployment
•	GitOps workflows
•	Kubernetes troubleshooting
