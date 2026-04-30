# 🔐 Kubernetes Security Hardening Guide (Production Ready)

This repository documents a **practical, production-grade Kubernetes security setup** using GitOps principles.

It covers **API security, runtime protection, policy enforcement, and observability**.

---

# 📌 Objectives

* Secure Kubernetes API access
* Enforce least privilege (RBAC)
* Prevent misconfigurations (policy engine)
* Detect runtime threats
* Enable monitoring and auditing
* Follow GitOps best practices

---

# 🧱 Architecture Overview

```
Kubernetes Cluster
│
├── 🔐 API Security
│   ├── Disable Anonymous Access
│   ├── RBAC (Role-Based Access Control)
│   └── Audit Logging
│
├── 🌐 Networking
│   ├── Ingress Controller (NGINX)
│   ├── TLS (cert-manager)
│   └── Network Policies
│
├── 🛡️ Security Layer
│   ├── Kyverno (Policy Engine)
│   ├── Falco (Runtime Security)
│   └── Vault (Secrets Management)
│
├── 📊 Observability
│   ├── Prometheus
│   ├── Grafana
│   └── Alertmanager
│
└── 🚀 GitOps
    └── ArgoCD (App of Apps)
```

---

# 🔐 1. API Server Security

## Disable Anonymous Access

Edit API server manifest:

```bash
sudo vi /etc/kubernetes/manifests/kube-apiserver.yaml
```

Add:

```yaml
- --anonymous-auth=false
```

### ✅ Verify

```bash
curl -k https://<API_SERVER>:6443
```

Expected:

```
401 Unauthorized
```

---

## Enable RBAC (Mandatory)

Ensure:

```yaml
--authorization-mode=Node,RBAC
```

---

# 🔑 2. RBAC (Least Privilege)

### Example Role

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: dev
  name: pod-reader
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "watch", "list"]
```

---

# 🌐 3. Network Security

## Default Deny Policy

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: default-deny
  namespace: default
spec:
  podSelector: {}
  policyTypes:
  - Ingress
  - Egress
```

---

# 🔒 4. TLS & Ingress

## Components

* ingress-nginx
* cert-manager

### Benefits

* HTTPS everywhere
* Automatic certificate renewal

---

# 🛡️ 5. Policy Enforcement (Kyverno)

## Install via ArgoCD (Helm)

Kyverno enforces rules like:

* No privileged containers
* Require resource limits
* Enforce labels

---

## Example Policy

```yaml
apiVersion: kyverno.io/v1
kind: ClusterPolicy
metadata:
  name: disallow-privileged
spec:
  validationFailureAction: enforce
  rules:
    - name: block-privileged
      match:
        resources:
          kinds:
            - Pod
      validate:
        message: "Privileged containers are not allowed"
        pattern:
          spec:
            containers:
              - securityContext:
                  privileged: false
```

---

# 🔍 6. Runtime Security (Falco)

## Detects:

* Reverse shells
* Suspicious processes
* Container escapes

## Install via Helm

```bash
helm repo add falcosecurity https://falcosecurity.github.io/charts
```

---

# 📊 7. Monitoring (Prometheus + Grafana)

## Stack

* kube-prometheus-stack
* Grafana dashboards
* Alertmanager

---

# 🔐 8. Secrets Management

## Vault Integration

* Store secrets securely
* Avoid hardcoding secrets in manifests

---

# 🔁 9. GitOps (ArgoCD)

## Pattern Used

* App of Apps (Platform)
* ApplicationSet (Apps - later)

---

## Benefits

* Declarative deployments
* Automatic sync
* Version control

---

# 🔍 10. Audit Logging (Recommended)

Enable in API server:

```yaml
--audit-log-path=/var/log/kubernetes/audit.log
```

---

# 🚨 11. Image Security (Next Step)

* Use Trivy for scanning
* Enforce signed images (Cosign + Kyverno)

---

# 📋 Production Checklist

| Area                      | Status |
| ------------------------- | ------ |
| Anonymous Access Disabled | ✅      |
| RBAC Enabled              | ✅      |
| Network Policies          | ✅      |
| TLS Enabled               | ✅      |
| Kyverno Installed         | ✅      |
| Falco Running             | ✅      |
| Monitoring Enabled        | ✅      |
| GitOps Setup              | ✅      |

---

# 🚀 Future Improvements

* External Secrets Operator (ESO)
* Loki for logging
* Multi-cluster GitOps
* Zero Trust networking (Cilium)

---

# 🧠 Key Takeaway

> Kubernetes security is not a single tool — it's a layered approach combining **access control, policy enforcement, runtime monitoring, and GitOps discipline**.

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