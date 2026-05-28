
---

# helm/README.md

```markdown
# Helm Charts

## Overview

This repository contains Helm charts and Helm-based deployments used in the Kubernetes HomeLab.

Helm is used for:

- Simplified Kubernetes application deployment
- Configuration templating
- Version-controlled deployments
- Package management
- Repeatable infrastructure provisioning

---

# Repository Structure

```text

.
├── charts/
├── values/
├── templates/
├── environments/
└── README.md
________________________________________
Common Commands
Add Repository

helm repo add bitnami https://charts.bitnami.com/bitnami
Install Chart

helm install nginx bitnami/nginx
Upgrade Chart

helm upgrade nginx bitnami/nginx
Remove Chart

helm uninstall nginx
________________________________________
Example values.yaml

replicaCount: 2

service:
  type: LoadBalancer
  port: 80
________________________________________
Planned Deployments
•	Prometheus
•	Grafana
•	Loki
•	Wazuh
•	ArgoCD
•	NGINX Ingress
•	Security tooling
________________________________________
Learning Areas
•	Helm templating
•	Kubernetes package management
•	GitOps workflows
•	Kubernetes automation
