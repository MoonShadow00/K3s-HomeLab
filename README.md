# Kubernetes HomeLab v1
> This project has been archived and is no longer under active development.
>
> Development has moved to Kubernetes HomeLab v2.
>
> While the cluster was functional, several architectural and networking decisions made during the build process created unnecessary complexity. Rather than continue iterating on the existing design, the environment was retired early to allow for a cleaner implementation based on lessons learned.

# Kubernetes HomeLab

## Overview

This repository documents my Kubernetes HomeLab environment built with K3s. The lab is designed for hands-on learning, testing, automation, networking, observability, and security engineering projects.

The environment focuses on:

* Kubernetes administration
* Infrastructure automation
* VLAN-aware networking
* Load balancing with MetalLB
* Containerized workloads
* Security engineering experimentation
* CI/CD and GitOps workflows
* Monitoring and observability

---

# HomeLab Goals

The purpose of this HomeLab is to:

* Develop production-aligned Kubernetes skills
* Build practical Security Engineering experience
* Experiment with networking and segmentation concepts
* Learn infrastructure automation and orchestration
* Simulate enterprise-style environments at small scale
* Host self-managed services and internal tooling
* Create portfolio projects for career growth

---

# Infrastructure

## Cluster Hardware

### Control Plane

| Node           | CPU                | RAM  | Storage   | Role          |
| -------------- | ------------------ | ---- | --------- | ------------- |
| k3s-control-01 | Intel Core i7-3770 | 12GB | 480GB SSD | Control Plane |

### Worker Nodes

| Node          | CPU                | RAM  | Storage | Role   |
| ------------- | ------------------ | ---  | ------- | ------ |
| k3s-worker-01 | Intel Core i7-3770 | 16GB | 1TB SSD | Worker |
| k3s-worker-02 | Intel Core i7-3770 | 16GB | 1TB SSD | Worker |
| k3s-worker-03 | Intel Core i7-3770 | 16GB | 1TB SSD | Worker |
| k3s-worker-04 | Intel Core i7-3770 | 16GB | 1TB SSD | Worker |

---

# Software Stack

| Component           | Purpose                             |
| ------------------- | ----------------------------------- |
| K3s                 | Lightweight Kubernetes distribution |
| Flannel             | Cluster networking (CNI)            |
| MetalLB             | Bare-metal load balancer            |
| Ubuntu Server 24.04 | Operating system                    |
| Docker / containerd | Container runtime                   |
| Helm                | Kubernetes package management       |
| GitHub              | Version control and documentation   |

---

# Networking

## Network Design

The HomeLab uses VLAN segmentation to separate management traffic, workloads, and services.

### VLAN Layout

| VLAN    | Purpose                     |
| ------- | --------------------------- |
| VLAN 10 | Management                  |
| VLAN 20 | Kubernetes Services         |
| VLAN 30 | Storage / Internal Services |

## Load Balancing

MetalLB is configured in Layer 2 mode to provide external IPs to Kubernetes services running on bare-metal infrastructure.

Example:

```yaml
apiVersion: metallb.io/v1beta1
kind: IPAddressPool
metadata:
  name: production-pool
  namespace: metallb-system
spec:
  addresses:
    - 10.10.20.100-10.10.20.120
```

---

# Cluster Architecture

```text
                     ┌─────────────────────┐
                     │      Router         │
                     └─────────┬───────────┘
                               │
                         VLAN Trunk
                               │
                     ┌─────────┴───────────┐
                     │      Switch         │
                     └─────────┬───────────┘
                               │
        ┌──────────────────────┼──────────────────────┐
        │                      │                      │
┌───────▼───────┐    ┌────────▼────────┐    ┌────────▼────────┐
│ Control Plane │    │   Worker Node   │    │   Worker Node   │
│ k3s-control   │    │ k3s-worker-01   │    │ k3s-worker-02   │
└───────────────┘    └─────────────────┘    └─────────────────┘
                               │
                     Additional Worker Nodes
```

---

# Features

## Current Features

* Multi-node K3s cluster
* VLAN-aware networking
* MetalLB load balancing
* Flannel CNI
* Persistent SSD-backed storage
* Git-based infrastructure tracking
* Ubuntu Server deployment

## Planned Features

* GitOps with ArgoCD
* Prometheus and Grafana monitoring
* Loki log aggregation
* Kubernetes security hardening
* SIEM integration
* Secrets management
* CI/CD pipelines
* Backup and disaster recovery
* Infrastructure-as-Code with Terraform

---

# Deployment

## Install K3s Control Plane

```bash
curl -sfL https://get.k3s.io | sh -
```

## Retrieve Node Token

```bash
sudo cat /var/lib/rancher/k3s/server/node-token
```

## Join Worker Nodes

```bash
curl -sfL https://get.k3s.io | K3S_URL=https://<CONTROL_PLANE_IP>:6443 K3S_TOKEN=<TOKEN> sh -
```

---

# Useful Commands

## View Cluster Nodes

```bash
kubectl get nodes -o wide
```

## View Pods

```bash
kubectl get pods -A
```

## Check Services

```bash
kubectl get svc -A
```

## Check MetalLB

```bash
kubectl get ipaddresspools -A
kubectl get l2advertisements -A
```

---

# Security Focus

This HomeLab is also used for cybersecurity and security engineering experimentation including:

* Network segmentation
* Firewall rule testing
* VPN technologies
* Kubernetes security hardening
* Identity and access management
* Log analysis
* Threat detection workflows
* Security monitoring pipelines

---

# Future Projects

Planned projects for this environment include:

* Kubernetes SIEM deployment
* Wazuh integration
* Security monitoring dashboards
* Honeypots and traffic analysis
* Internal developer platform concepts
* Zero Trust networking experiments
* Cloud-native security tooling

---

# Repository Structure

```text
.
├── manifests/
├── helm/
├── networking/
├── monitoring/
├── security/
├── scripts/
├── docs/
└── README.md
```

---

# Learning Objectives

This HomeLab supports continuous learning in:

* Kubernetes
* Linux administration
* Networking
* Cybersecurity
* Infrastructure automation
* Cloud-native tooling
* DevOps practices
* Observability engineering

---

# Author

## Kwano Mathebula

Network Engineer transitioning into Security Engineering.

Areas of interest:

* Kubernetes
* Network Security
* Cybersecurity
* Infrastructure Automation
* SD-WAN
* VPN Technologies
* Cloud-native Security

---

# License

This project is licensed under the MIT License.
