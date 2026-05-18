# Enterprise DevSecOps GitOps Platform on Kubernetes

![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![ArgoCD](https://img.shields.io/badge/ArgoCD-EF7B4D?style=for-the-badge&logo=argo&logoColor=white)
![Kyverno](https://img.shields.io/badge/Kyverno-326CE5?style=for-the-badge)
![Falco](https://img.shields.io/badge/Falco-00AEEF?style=for-the-badge)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=for-the-badge&logo=prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=for-the-badge&logo=grafana&logoColor=white)
![Harbor](https://img.shields.io/badge/Harbor-60B932?style=for-the-badge)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white)

Enterprise-grade DevSecOps platform built on Kubernetes using GitOps, policy-as-code, supply chain security, progressive delivery, observability, and runtime threat detection.

---

# Platform Overview

This project demonstrates a production-style Kubernetes DevSecOps platform running on a multi-node kubeadm cluster provisioned with Vagrant.

The platform follows GitOps principles using ArgoCD and integrates multiple security layers across the software delivery lifecycle including:

- Supply chain security
- Policy enforcement
- Runtime security
- Progressive delivery
- Secret management
- Observability
- Automated GitOps deployment

---

# Architecture Diagram

![Architecture](assets/architecture.png)

---

# Key Features

## GitOps Deployment
- ArgoCD-based GitOps workflow
- Multi-environment deployment strategy
- Automated sync and reconciliation
- Declarative Kubernetes infrastructure

## Kubernetes Security
- Kyverno policy enforcement
- Image signature verification
- Resource validation policies
- Non-root enforcement
- Privileged container blocking
- Latest tag prevention
- HostPath restriction policies

## Runtime Security
- Falco runtime threat detection
- Kubernetes audit monitoring
- Container activity monitoring

## Supply Chain Security
- Trivy vulnerability scanning
- SBOM generation
- Cosign image signing
- Harbor registry integration
- Signed container image verification

## Progressive Delivery
- Argo Rollouts canary deployments
- Controlled rollout strategy
- Automated rollback support

## Secrets Management
- External Secrets Operator integration
- Vault-based secret management
- Centralized secret storage

## Observability Stack
- Prometheus monitoring
- Grafana dashboards
- Kyverno metrics integration
- Kubernetes cluster monitoring

---

# Technology Stack

| Category | Tools |
|---|---|
| Container Orchestration | Kubernetes (kubeadm) |
| GitOps | ArgoCD |
| Progressive Delivery | Argo Rollouts |
| Policy Enforcement | Kyverno |
| Runtime Security | Falco |
| Secrets Management | Vault + External Secrets Operator |
| Monitoring | Prometheus + Grafana |
| Container Registry | Harbor |
| CI/CD | GitHub Actions |
| Security Scanning | Trivy |
| Image Signing | Cosign |
| Code Quality | SonarCloud |
| Infrastructure | Vagrant + VirtualBox |

---

# Repository Structure

```bash
.
├── assets
│   ├── architecture.png
│   ├── demo-01.gif
│   └── demo-02.gif
├── bootstrap
│   ├── infra-root.yaml
│   └── platform-app.yaml
├── infra
│   ├── applications
│   │   ├── kustomization.yaml
│   │   ├── kyverno-policies-app
│   │   │   ├── application.yaml
│   │   │   └── kustomization.yaml
│   │   ├── network-policies-app
│   │   ├── rbac-app
│   │   │   ├── application.yaml
│   │   │   └── kustomization.yaml
│   │   └── vault-app
│   │       ├── application.yaml
│   │       └── kustomization.yaml
│   ├── kustomization.yaml
│   ├── manifests
│   │   ├── kyverno-policies
│   │   │   ├── base
│   │   │   │   ├── clusterpolicy
│   │   │   │   │   ├── allowed-registries.yaml
│   │   │   │   │   ├── disallow-hostpath.yaml
│   │   │   │   │   ├── disallow-latest-tag.yaml
│   │   │   │   │   ├── disallow-privileged-containers.yaml
│   │   │   │   │   ├── disallow-privilege-escalation.yaml
│   │   │   │   │   ├── kustomization.yaml
│   │   │   │   │   ├── require-non-root.yaml
│   │   │   │   │   ├── require-probes.yaml
│   │   │   │   │   ├── require-resources.yaml
│   │   │   │   │   └── verify-keyless-signatures.yaml
│   │   │   │   └── kustomization.yaml
│   │   │   ├── kustomization.yaml
│   │   │   └── patch.yaml
│   │   ├── network-policies
│   │   ├── rbac
│   │   │   ├── base
│   │   │   │   ├── external-secrets-rbac.yaml
│   │   │   │   ├── falco-rbac.yaml
│   │   │   │   ├── kustomization.yaml
│   │   │   │   ├── kyverno-rbac.yaml
│   │   │   │   └── monitoring-rbac.yaml
│   │   │   └── kustomization.yaml
│   │   └── vault
│   │       ├── base
│   │       │   ├── cluster-role-binding.yaml
│   │       │   ├── cluster-sa.yaml
│   │       │   ├── clustersecretstore.yaml
│   │       │   ├── cluster-token.yaml
│   │       │   ├── kustomization.yaml
│   │       │   ├── secret-crb.yaml
│   │       │   ├── secret-sa.yaml
│   │       │   ├── secretstore-dev.yaml
│   │       │   └── secret-token.yaml
│   │       └── kustomization.yaml
│   └── projects
│       ├── k8s-infra-project.yaml
│       └── kustomization.yaml
├── platform
│   ├── applications
│   │   ├── argo-rollouts
│   │   │   └── application.yaml
│   │   ├── cert-manager
│   │   │   └── application.yaml
│   │   ├── external-secrets
│   │   │   └── application.yaml
│   │   ├── falco
│   │   │   └── application.yaml
│   │   ├── ingress-nginx
│   │   │   └── application.yaml
│   │   ├── kustomization.yaml
│   │   ├── kyverno
│   │   │   └── application.yaml
│   │   ├── metrics-server
│   │   │   └── application.yaml
│   │   └── monitoring
│   │       └── application.yaml
│   ├── kustomization.yaml
│   └── projects
│       ├── k8s-observability.yaml
│       ├── k8s-platform.yaml
│       ├── k8s-security.yaml
│       └── kustomization.yaml
└── README.md
```

---

# Platform Components

## Platform Services

| Component | Purpose |
|---|---|
| ArgoCD | GitOps continuous delivery |
| Kyverno | Kubernetes policy engine |
| Falco | Runtime threat detection |
| Harbor | Secure image registry |
| External Secrets Operator | Secret synchronization |
| Vault | Centralized secret management |
| Argo Rollouts | Progressive delivery |
| Metrics Server | Kubernetes resource metrics |
| Prometheus | Metrics collection |
| Grafana | Visualization dashboards |

---

# Security Policies

The platform enforces multiple Kyverno security policies including:

- Allowed container registries
- Require resource requests and limits
- Require liveness/readiness probes
- Prevent privileged containers
- Prevent privilege escalation
- Require non-root containers
- Block latest image tags
- Block hostPath volumes
- Verify signed container images

---

# Kyverno Policy Demo

![Kyverno Demo](assets/demo-02.gif)

---

## ArgoCD GitOps Dashboard

![ArgoCD GitOps Dashboard](assets/demo-01.gif)

---

# Monitoring Stack

Grafana dashboards integrated with Prometheus and Kyverno metrics.

![Monitoring](assets/grafana-dashboards-kyverno.gif)

---

# Deployment Environment

## Kubernetes Cluster
- kubeadm-based Kubernetes cluster
- Multi-node environment
- Hosted locally using Vagrant and VirtualBox

## CI/CD Environment
- GitHub Actions
- Self-hosted runners

---

# Related Repositories

## Application Source Repository
https://github.com/Ajaz3800/devsecops-app

## GitOps Deployment Repository
https://github.com/Ajaz3800/devsecops-gitops

---

# Future Improvements

- Falco alert forwarding integration
- Slack/Discord alerting
- Service mesh integration
- Multi-cluster GitOps management
- OPA Gatekeeper comparison
- Advanced SLO monitoring
- Automated incident response

---

# Learning Outcomes

This project helped strengthen practical knowledge in:

- Kubernetes Administration
- DevSecOps
- GitOps Workflows
- Policy-as-Code
- Supply Chain Security
- Runtime Security
- CI/CD Automation
- Kubernetes Observability
- Progressive Delivery

---


## ⭐ Support

If you find this project helpful, please give it a star ⭐ on GitHub.

---

## 🌐 Connect With Me

<div align="center">
  
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/shaikh-muhammad-ajaz)
[![Email](https://img.shields.io/badge/Email-shaikhajaz38000@gmail.com-red?style=for-the-badge&logo=gmail&logoColor=white)](mailto:shaikhajaz38000@gmail.com)
[![YouTube](https://img.shields.io/badge/YouTube-Subscribe-red?style=for-the-badge\&logo=youtube\&logoColor=white)](https://www.youtube.com/@devopswithajaz)
</div>

<div align="center">

[![Upwork](https://img.shields.io/badge/Upwork-Hire%20Me-6FDA44?style=for-the-badge&logo=upwork&logoColor=white)](https://upwork.com/freelancers/muhammadajaz)
[![Fiverr](https://img.shields.io/badge/Fiverr-Order%20Now-1DBF73?style=for-the-badge&logo=fiverr&logoColor=white)](https://www.fiverr.com/ajazshaikh3800)
</div>

---

<div align="center">
  
### 💡 "Turning ideas into production-ready systems."

![Profile Views](https://komarev.com/ghpvc/?username=Ajaz3800&color=brightgreen&style=flat-square)
[![GitHub followers](https://img.shields.io/github/followers/Ajaz3800?label=Follow&style=social)](https://github.com/Ajaz3800)

</div>