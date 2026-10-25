# Zero-Trust Kubernetes GitOps

Hardened multi-tenant Kubernetes (AKS/EKS) cluster with strict ArgoCD GitOps, Cilium eBPF security, and HashiCorp Vault secrets.

## Security Layers
1. **Cilium eBPF** - Default-deny network policies, L7 HTTP filtering
2. **OPA Gatekeeper** - Admission webhooks enforcing policy
3. **Vault External Secrets** - No secrets in Git, ever
4. **Cosign** - Container image signature verification
5. **ArgoCD** - GitOps-only deployments, no kubectl in CI

## Cluster Bootstrap

```bash
# 1. Install ArgoCD
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# 2. Apply App-of-Apps
kubectl apply -f argocd/app-of-apps.yaml

# 3. ArgoCD auto-deploys: Cilium, Gatekeeper, Vault ESO, and all apps
```
