---
id: RBK-0005
type: runbook
title: Migrate Service from Podman to AKS + ArgoCD
domain: podman, argocd
platforms: [podman, argocd+aks]
severity: sev-3
status: published
owner: platform-enablement
created: 2026-04-08
updated: 2026-04-08
tags: [migration, containerization, podman, argocd, aks, step-by-step]
related_ids: [INC-0030, INC-0031, INC-0032, DG-0001, DG-0002, DG-0003]
error_signatures: []
---

# Runbook: Migrate Service from Podman to AKS + ArgoCD

## Summary

Move a locally containerized service (running on Podman) to production on Azure Kubernetes Service (AKS) with ArgoCD as the deployment orchestrator. This guide covers containerization validation, registry setup, AKS deployment, and ArgoCD integration.

## Prerequisites

Before starting, ensure you have:
- [ ] Service runs locally on Podman without errors
- [ ] Podman image builds successfully
- [ ] Access to Azure subscription and AKS cluster
- [ ] Azure Container Registry (ACR) created and accessible
- [ ] ArgoCD installed and running on the target AKS cluster
- [ ] Git repository for Application manifests
- [ ] `az`, `kubectl`, `argocd`, and `podman` CLIs installed

## Step-by-Step Migration

### Phase 1 — Validate Local Podman Container

**Step 1: Verify Podman image builds and runs locally**
- [ ] Confirm Dockerfile exists and is valid
- [ ] Build image locally
- [ ] Run container and test endpoints

```bash
# Build the Podman image
podman build -t <service-name>:<version> .

# Run and test locally
podman run -d -p 8080:8080 --name test-<service-name> <service-name>:<version>

# Test health endpoint
curl http://localhost:8080/health

# Stop test container
podman stop test-<service-name>
podman rm test-<service-name>
```

**Verify:**
```bash
podman images | grep <service-name>
# Should show image with version tag
```

Expected output: Image listed with correct tag and size.

---

### Phase 2 — Push Container Image to Azure Container Registry

**Step 2: Authenticate to ACR**
- [ ] ACR name and login credentials ready
- [ ] Docker credentials configured

```bash
# Login to Azure
az login

# Get ACR login server
ACR_LOGIN_SERVER=$(az acr show --resource-group <rg-name> --name <acr-name> --query loginServer -o tsv)

# Login to ACR
az acr login --name <acr-name>
```

**Step 3: Tag and push image to ACR**
- [ ] Image tagged with ACR fully qualified name
- [ ] Image successfully pushed

```bash
# Tag for ACR
podman tag <service-name>:<version> $ACR_LOGIN_SERVER/<service-name>:<version>

# Push to ACR
podman push $ACR_LOGIN_SERVER/<service-name>:<version>
```

**Verify:**
```bash
az acr repository show --resource-group <rg-name> --name <acr-name> --repository <service-name>
# Should show image tags
```

Expected output: Repository and image tags listed in ACR.

---

### Phase 3 — Create Kubernetes Namespace and Provision Prerequisites

**Step 4: Request namespace creation from DevOps**
- [ ] DevOps has created namespace
- [ ] Namespace is accessible

```bash
# Ask DevOps to run:
# kubectl create namespace <your-namespace>
# kubectl label namespace <your-namespace> team=<your-team> env=prod

# Verify namespace exists
kubectl get ns <your-namespace>
```

**Step 5: Create Kubernetes Secret for ACR image pull**
- [ ] Secret created in target namespace
- [ ] Secret allows AKS to pull from ACR

```bash
# Get ACR credentials
ACR_PASSWORD=$(az acr credential show --resource-group <rg-name> --name <acr-name> --query passwords[0].value -o tsv)

# Create image pull secret in target namespace
kubectl create secret docker-registry acr-secret \
  --docker-server=$ACR_LOGIN_SERVER \
  --docker-username=<acr-name> \
  --docker-password=$ACR_PASSWORD \
  --docker-email=deployment@<your-org>.com \
  -n <your-namespace>
```

**Verify:**
```bash
kubectl get secret acr-secret -n <your-namespace>
```

Expected output: Secret exists with type `kubernetes.io/dockercfg`.

---

### Phase 4 — Create Kubernetes Deployment Manifest

**Step 6: Write Kubernetes Deployment manifest**
- [ ] Manifest created with correct image reference
- [ ] Resource limits and env vars configured
- [ ] Health probes configured

**File: `deployment.yaml`**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: <service-name>
  namespace: <your-namespace>
spec:
  replicas: 2
  selector:
    matchLabels:
      app: <service-name>
  template:
    metadata:
      labels:
        app: <service-name>
    spec:
      imagePullSecrets:
        - name: acr-secret
      containers:
      - name: <service-name>
        image: <ACR_LOGIN_SERVER>/<service-name>:<version>
        ports:
        - containerPort: 8080
        resources:
          requests:
            memory: "256Mi"
            cpu: "250m"
          limits:
            memory: "512Mi"
            cpu: "500m"
        livenessProbe:
          httpGet:
            path: /health
            port: 8080
          initialDelaySeconds: 10
          periodSeconds: 10
        readinessProbe:
          httpGet:
            path: /ready
            port: 8080
          initialDelaySeconds: 5
          periodSeconds: 5
---
apiVersion: v1
kind: Service
metadata:
  name: <service-name>
  namespace: <your-namespace>
spec:
  selector:
    app: <service-name>
  ports:
  - port: 80
    targetPort: 8080
  type: ClusterIP
```

### Phase 5 — Deploy with ArgoCD

**Step 7: Request ArgoCD prerequisite setup from DevOps**
- [ ] DevOps has registered target cluster in ArgoCD
- [ ] DevOps has granted Project RBAC for your team
- [ ] Repository path is in Project sourceRepos

```bash
# DevOps should have run:
# argocd cluster add <kube-context> --name <cluster-name>
# argocd proj add-source <project-name> <git-repo-url>
# argocd proj add-destination <project-name> <cluster-name> <your-namespace>
```

**Step 8: Create ArgoCD Application manifest**
- [ ] Git repo path contains deployment.yaml
- [ ] Application references correct destination
- [ ] Sync policy configured

**File: `argocd-app.yaml` (commit to Git repo)**
```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: <service-name>
  namespace: argocd
spec:
  project: <project-name>
  source:
    repoURL: <git-repo-url>
    targetRevision: main
    path: k8s/<service-name>
  destination:
    server: https://kubernetes.default.svc
    namespace: <your-namespace>
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
    syncOptions:
    - CreateNamespace=false
```

**Step 9: Apply ArgoCD Application**
- [ ] Application created in ArgoCD
- [ ] Initial sync triggered

```bash
# Commit and push argocd-app.yaml to Git

# Apply to ArgoCD (or let ArgoCD auto-discover if using app-of-apps pattern)
kubectl apply -f argocd-app.yaml
```

**Verify:**
```bash
argocd app get <service-name>
# Should show: Status=Syncing then Status=Synced, Health=Healthy
```

---

### Phase 6 — Final Migration Validation

**Step 10: Verify deployment is healthy**
- [ ] Pod is running
- [ ] Health probes pass
- [ ] Service endpoint is reachable

```bash
# Check deployment status
kubectl get deployment <service-name> -n <your-namespace>

# Check pod status
kubectl get pods -n <your-namespace> -l app=<service-name>

# Check service endpoint
kubectl get service <service-name> -n <your-namespace>

# Verify ArgoCD is synced
argocd app get <service-name>

# Test service health
POD_IP=$(kubectl get pod -n <your-namespace> -l app=<service-name> -o jsonpath='{.items[0].status.podIP}')
curl http://$POD_IP:8080/health
```

Expected results:
- Pod status: `Running`
- ArgoCD status: `Synced` and `Healthy`
- Health endpoint responds with 200

---

## Post-Migration Validation

Run this final checklist:

```bash
# 1. Pod count is correct
kubectl get deployment <service-name> -n <your-namespace> | grep READY

# 2. No failed containers
kubectl get pods -n <your-namespace> -l app=<service-name> | grep -v Running && echo "WARNING: Failed pods detected"

# 3. ArgoCD app is healthy
argocd app get <service-name> | grep -E "Status|Health"

# 4. Service logs are clean
kubectl logs -n <your-namespace> -l app=<service-name> --tail=20
```

Expected results:
- Deployment shows desired replicas running
- All pods in `Running` state
- ArgoCD status: `Synced`, Health: `Healthy`
- No error messages in logs

---

## Rollback

If deployment fails or needs to rollback to Podman:

```bash
# Delete ArgoCD Application (this removes K8s resources)
argocd app delete <service-name>

# Or scale to 0 without deleting
kubectl scale deployment <service-name> -n <your-namespace> --replicas=0

# Restart local Podman container
podman run -d -p 8080:8080 --name <service-name> <acr_login_server>/<service-name>:<version>
```

---

## Common Issues

| Error | Cause | Fix |
|---|---|---|
| ImagePullBackOff | ACR secret not created or incorrect credentials | Recreate secret with correct ACR credentials |
| PermissionDenied from ArgoCD | Project RBAC not configured | Ask DevOps to add namespace/repo to Project |
| Pod CrashLoopBackOff | Liveness probe failing | Check logs: `kubectl logs <pod> -n <namespace>` |
| Health endpoint returns 500 | Application misconfiguration in container | Verify Dockerfile EXPOSE matches container port |

---

## Related Artifacts

- Incident: [INC-0030 — Podman image pull failure](../incidents/incident-inc-0030-podman-image-pull.md)
- Doc Gap: [DG-0001 — Namespace not pre-provisioned](../doc-gaps/docgap-dg-0001-argocd-namespace-not-preprovisioned.md)
- Doc Gap: [DG-0002 — Cluster not registered](../doc-gaps/docgap-dg-0002-argocd-cluster-not-registered.md)
- Runbook: [RBK-0004 — Platform onboarding quick steps](runbook-rbk-0004-platform-onboarding-quick-steps.md)
