# AKS Kubernetes Platform Engineering

> Production-grade Azure Kubernetes Service (AKS) platform setup with GitOps, service mesh, and enterprise security hardening.

---

## Platform Components

| Component | Tool | Purpose |
|---|---|---|
| GitOps | ArgoCD | Declarative continuous deployment |
| Service Mesh | Istio | mTLS, traffic management, observability |
| Ingress | NGINX / App Gateway | External traffic routing with WAF |
| Secrets | Azure Key Vault CSI | Zero-secret-in-YAML policy |
| Monitoring | Prometheus + Grafana | Metrics, dashboards, alerting |
| Policy | OPA Gatekeeper | Kubernetes admission control |
| Network | Calico / Azure CNI | Network policies, micro-segmentation |

## Security Hardening Applied

- RBAC with namespace-scoped service accounts
- Network Policies blocking all default inter-namespace traffic
- Pod Security Standards - Restricted profile enforced
- OPA Gatekeeper - no privileged containers, no root, resource limits required
- Azure Key Vault CSI Driver - zero secrets in manifests
- Workload Identity (Managed Identity) for pod-level Azure RBAC
- Istio mTLS - all service-to-service traffic encrypted
- Image pull from private ACR only (deny public registries via Gatekeeper)

## Quick Start

`ash
az aks get-credentials --resource-group rg-aks-prod --name aks-prod-001
kubectl apply -k argocd/
kubectl apply -k platform/
argocd app sync --all
`

---
Senior DevOps Engineer - Vikas Rao