# Kubernetes HomeLab Networking

## Overview

This repository contains the networking architecture, configurations, and deployment documentation for my Kubernetes HomeLab environment.

The primary goal of this repository is to document and manage:

* VLAN segmentation
* K3s networking
* MetalLB configuration
* Ubuntu network configuration
* Layer 2 load balancing
* Internal routing concepts
* Security-focused network design
* Bare-metal Kubernetes networking

---

# Objectives

This networking repository exists to:

* Develop enterprise-style networking skills
* Build practical Kubernetes networking experience
* Learn VLAN and segmentation design
* Experiment with network security concepts
* Document reusable infrastructure configurations
* Simulate production networking environments
* Create portfolio-ready networking projects

---

# Environment Overview

## Kubernetes Distribution

| Component        | Technology          |
| ---------------- | ------------------- |
| Kubernetes       | K3s                 |
| CNI              | Flannel             |
| Load Balancer    | MetalLB             |
| Operating System | Ubuntu Server 24.04 |

---

# Physical Infrastructure

## Cluster Hardware

### Control Plane

| Node           | CPU                | RAM  | Storage   |
| -------------- | ------------------ | ---- | --------- |
| k3s-control-01 | Intel Core i7-3770 | 12GB | 480GB SSD |

### Worker Nodes

| Node          | CPU                | RAM | Storage |
| ------------- | ------------------ | --- | ------- |
| k3s-worker-01 | Intel Core i7-3770 | 8GB | 1TB SSD |
| k3s-worker-02 | Intel Core i7-3770 | 8GB | 1TB SSD |
| k3s-worker-03 | Intel Core i7-3770 | 8GB | 1TB SSD |
| k3s-worker-04 | Intel Core i7-3770 | 8GB | 1TB SSD |

---

# Network Architecture

## High-Level Design

```text
                     ┌──────────────────────┐
                     │        Router        │
                     └──────────┬───────────┘
                                │
                           VLAN Trunk
                                │
                     ┌──────────┴───────────┐
                     │       Switch         │
                     └──────────┬───────────┘
                                │
          ┌─────────────────────┼─────────────────────┐
          │                     │                     │
 ┌────────▼────────┐  ┌────────▼────────┐  ┌────────▼────────┐
 │  Control Plane  │  │   Worker Node   │  │   Worker Node   │
 │  k3s-control    │  │ k3s-worker-01   │  │ k3s-worker-02   │
 └─────────────────┘  └─────────────────┘  └─────────────────┘
```

---

# VLAN Design

The HomeLab uses VLAN segmentation to isolate workloads and improve security.

## VLAN Layout

| VLAN    | Purpose                     | Example Subnet |
| ------- | --------------------------- | -------------- |
| VLAN 10 | Management                  | 10.10.10.0/24  |
| VLAN 20 | Kubernetes Services         | 10.10.20.0/24  |
| VLAN 30 | Internal Services / Storage | 10.10.30.0/24  |

---

# Ubuntu Netplan Configuration

Example VLAN trunk configuration:

```yaml
network:
  version: 2
  ethernets:
    eno1:
      dhcp4: false

  vlans:
    eno1.10:
      id: 10
      link: eno1
      addresses:
        - 10.10.10.10/24
      routes:
        - to: default
          via: 10.10.10.1

    eno1.20:
      id: 20
      link: eno1
      addresses:
        - 10.10.20.10/24

    eno1.30:
      id: 30
      link: eno1
      addresses:
        - 10.10.30.10/24
```

Apply configuration:

```bash
sudo netplan apply
```

---

# Kubernetes Networking

## Cluster CIDRs

| Network         | CIDR         |
| --------------- | ------------ |
| Pod Network     | 10.42.0.0/16 |
| Service Network | 10.43.0.0/16 |

## CNI

Flannel is used as the Container Network Interface (CNI) for inter-pod communication.

Features:

* Lightweight
* Simple deployment
* K3s native integration
* VXLAN support

---

# MetalLB Configuration

MetalLB is configured in Layer 2 mode for bare-metal service exposure.

## IP Address Pool

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

## L2 Advertisement

```yaml
apiVersion: metallb.io/v1beta1
kind: L2Advertisement
metadata:
  name: l2-advertisement
  namespace: metallb-system
spec:
  ipAddressPools:
    - production-pool
```

---

# Service Exposure

Example LoadBalancer service:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: LoadBalancer
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
```

---

# Security Considerations

The network architecture is designed with security segmentation principles in mind.

## Security Areas

* VLAN isolation
* Controlled east-west traffic
* Segmented management networks
* Firewall rule testing
* Kubernetes network exposure management
* Internal service isolation
* Principle of least privilege networking

---

# Troubleshooting

## Verify VLAN Interfaces

```bash
ip a
```

## Check Routes

```bash
ip route
```

## Verify MetalLB

```bash
kubectl get pods -n metallb-system
kubectl logs -n metallb-system -l app=metallb
```

## Check Node Status

```bash
kubectl get nodes -o wide
```

## Test Connectivity

```bash
ping <TARGET_IP>
```

---

# Repository Structure

```text
.
├── netplan/
├── metallb/
├── flannel/
├── vlan-configs/
├── diagrams/
├── troubleshooting/
├── manifests/
└── README.md
```

---

# Future Improvements

Planned improvements include:

* BGP-based MetalLB deployment
* NetworkPolicy implementation
* Calico testing
* Cilium evaluation
* Kubernetes ingress architecture
* Service mesh experimentation
* IDS/IPS integration
* Network observability tooling
* eBPF experimentation

---

# Learning Focus

This repository supports practical learning in:

* Kubernetes networking
* Linux networking
* VLAN design
* Bare-metal Kubernetes
* Layer 2 networking
* Infrastructure troubleshooting
* Security engineering
* Network segmentation
* Cloud-native networking

---

# Author

## Kwano Mathebula

Network Engineer transitioning into Security Engineering.

Special interests:

* Kubernetes
* SD-WAN
* VPN Technologies
* Infrastructure Security
* Network Automation
* Cloud-native Security
* Bare-metal Kubernetes

---

# License

This project is licensed under the MIT License.
