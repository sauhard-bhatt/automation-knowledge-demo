---
id: RBK-0006
type: runbook
title: Adopt ArgoCD for Existing AKS Service
domain: argocd
platforms: [argocd+aks]
severity: sev-3
status: published
owner: platform-enablement
created: 2026-04-08
updated: 2026-04-08
tags: [migration, argocd-adoption, gitops, step-by-step]
related_ids: [DG-0001, DG-0002, DG-0003, INC-0001, INC-0003, INC-0004]
error_signatures: []
---

# Runbook: Adopt ArgoCD for Existing AKS Service

## Summary

Move an existing service that is deployed manually or via other tools (kubectl apply, Helm, Kustomize) to be managed by ArgoCD. This enables GitOps workflow: changes to Git automatically sync to the cluster.

## Prerequisites

Before starting, ensure you have:
- [ ] Service is currently running on AKS cluster
- [ ] Service Kubernetes manifests (YAML files) exist or can be exported
- [ ] Git repository ready to store manifests
- [ ] ArgoCD installed on the AKS cluster
- [ ] Access to the AKS cluster (kubectl)
- [ ] Access to ArgoCD control plane
- [ ] `git`, `kubectl`, and `argocd` CLIs installed
- [ ] Target namespace exists (or will be created by ArgoCD)

## Step-by-Step Migration

### Phase 1 — Audit Current Deployment

**Step 1: Document current running state**
- [ ] Current manifests identified
- [ ] Resource list captured
- [ ] Service endpoint recorded

```bash
# List all resources currently deployed
kubectl get all -n <your-namespace>

# Export current deployment YAML
kubectl get deployment <service-name> -n <your-namespace> -o yaml > deployment-backup.yaml
kubectl get service <service-name> -n <your-namespace> -o yaml > service-backup.yaml
kubectl get configmap -n <your-namespace> -o yaml > configmap-backup.yaml
kubectl get secret -n <your-namespace> -o yaml > secret-backup.yaml (be careful with secrets!)

# Record current replicas and endpoints
kubectl get deployment <service-name> -n <your-namespace> -o jsonpath='{.spec.replicas}'
```

**Verify:**
```bash
# Confirm service is accessible
SVCIP=$(kubectl get service <service-name> -n <your-namespace> -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
curl http://$SVCIP/health
```

Expected output: Service responds with 200 status.

---

### Phase 2 — Prepare Git Repository with Manifests

**Step 2: Create Git directory structure**
- [ ] Git repo directory ready
- [ ] Manifests organized by service

```bash
# Clone or navigate to Git repo
cd <git-repo>
mkdir -p manifests/<service-name>

# Copy exported manifests to Git repo
cp deployment-backup.yaml manifests/<service-name>/
cp service-backup.yaml manifests/<service-name>/
cp configmap-backup.yaml manifests/<service-name>/
```

**Step 3: Clean and normalize manifests for GitOps**
- [ ] Remove status fields and metadata
- [ ] Externalize secrets (move to sealed secrets or external vault)
- [ ] Use configurable values (environment variables, ConfigMaps)
- [ ] Add labels for ArgoCD tracking

**File: `manifests/<service-name>/deployment.yaml`**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: <service-name>
  namespace: <your-namespace>
  labels:
    app: <service-name>
    managed-by: argocd
spec:
  replicas: 2  # Can be overridden via ArgoCD
  selector:
    matchLabels:
      app: <service-name>
  template:
    metadata:
      labels:
        app: <service-name>
    spec:
      containers:
      - name: <service-name>
        image: <registry>/<service-name>:latest
        ports:
        - containerPort: 8080
        livenessProbe:
          httpGet:
            path: /health
            port: 8080
          initialDelaySeconds: 10
          periodSeconds: 10
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
  type: LoadBalancer
```

**Step 4: Commit manifests to Git**
- [ ] Manifests committed
- [ ] Branch is main or target branch

```bash
git add manifests/<service-name>/
git commit -m "feat: initial commit of <service-name> manifests for ArgoCD adoption"
git push origin main
```

**Verify:**
```bash
# Confirm files are in Git
git ls-files | grep manifests/<service-name>/
```

Expected output: List of manifest files in Git.

---

### Phase 3 — Request ArgoCD Prerequisites from DevOps

**Step 5: Ensure cluster is registered and RBAC is configured**
- [ ] DevOps confirms cluster is registered in ArgoCD
- [ ] DevOps confirms Project includes your repo and namespace

```
Send to DevOps:

"Please confirm / set up the following for ArgoCD adoption:
1. Target cluster <cluster-name> is registered in ArgoCD
2. ArgoCD Project <project-name> includes:
   - Source repo: <git-repo-url>
   - Destination: cluster <cluster-name>, namespace <your-namespace>
   - Role permissions for my team"

DevOps runs:
argocd cluster list  # Verify cluster exists
argocd proj get <project-name>  # Verify repo and destination
```

---

### Phase 4 — Create ArgoCD Application

**Step 6: Create ArgoCD Application manifest**
- [ ] Application manifest written
- [ ] Source and destination configured
- [ ] Sync policy set to automated with pruning

**File: `argocd-app.yaml` (apply once, then stored in Git or ArgoCD UI)**
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
    path: manifests/<service-name>
  destination:
    server: https://kubernetes.default.svc  # or <cluster-url>
    namespace: <your-namespace>
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
    syncOptions:
    - CreateNamespace=false
  # Optional: Enable periodic refresh 
  revisionHistoryLimit: 10
```

**Step 7: Apply ArgoCD Application**
- [ ] Application created in ArgoCD
- [ ] Initial sync started

```bash
# Create the Application in ArgoCD
kubectl apply -f argocd-app.yaml

# Watch sync progress
argocd app wait <service-name> --sync
```

**Verify:**
```bash
argocd app get <service-name>
# Should show:
# - Status: Synced
# - Health: Healthy
# - Sync Policy: Automatic
```

Expected output:
```
Name:               <service-name>
Project:            <project-name>
Status:             Synced
Health:             Healthy
Repo:               <git-repo-url>
Path:               manifests/<service-name>
```

---

### Phase 5 — Trigger Cutover (Old Deployment → ArgoCD-Managed)

**Step 8: Delete old manually-deployed resources**
- [ ] Verified ArgoCD Application is Synced
- [ ] Understood that deleting old objects will cause brief downtime
- [ ] Prepared rollback plan

⚠️ **WARNING**: If old deployment and ArgoCD app both exist, they may conflict. You must delete the old one.

```bash
# Option 1: Scale down old deployment (safest first step)
kubectl scale deployment <service-name>-old -n <your-namespace> --replicas=0

# Option 2: Delete old deployment entirely (after confirming ArgoCD pod is running)
kubectl delete deployment <service-name>-old -n <your-namespace>

# Verify ArgoCD-managed pod is running
kubectl get pods -n <your-namespace> -l app=<service-name>
```

**Step 9: Verify cutover success**
- [ ] ArgoCD pod is healthy
- [ ] Service endpoint is accessible
- [ ] No errors in logs

```bash
# Check ArgoCD-managed deployment
kubectl get deployment <service-name> -n <your-namespace>

# Check pod status
kubectl get pods -n <your-namespace> -l app=<service-name>

# Test service endpoint
curl http://$(kubectl get service <service-name> -n <your-namespace> -o jsonpath='{.status.loadBalancer.ingress[0].ip}')/health
```

Expected results:
- Deployment shows desired replicas running
- Pods in `Running` state
- Service responds with 200

---

### Phase 6 — Test GitOps Workflow

**Step 10: Make a test change in Git**
- [ ] Changed a manifest in Git
- [ ] Committed and pushed
- [ ] ArgoCD auto-synced

```bash
# Edit a manifest (e.g., increase replicas)
sed -i 's/replicas: 2/replicas: 3/' manifests/<service-name>/deployment.yaml

# Commit and push
git add manifests/<service-name>/deployment.yaml
git commit -m "test: increase replicas to 3"
git push origin main

# Wait a few seconds for ArgoCD to sync
sleep 5

# Verify replicas increased
kubectl get deployment <service-name> -n <your-namespace> -o jsonpath='{.spec.replicas}'
# Should show: 3
```

**Verify:**
```bash
argocd app get <service-name> | grep -E "Status|Repo|LastSync"
# Status should be Synced, timestamp should be recent
```

Expected output:
```
Status:      Synced
Repo:        <git-repo-url>
LastSync:    2026-04-08T14:32:15Z
```

---

## Post-Migration Validation

Run this final checklist:

```bash
# 1. Deployment is ArgoCD-managed
kubectl get deployment <service-name> -n <your-namespace> -o jsonpath='{.metadata.labels}' | grep argocd
# Should show: managed-by=argocd

# 2. Pod health is good
kubectl get pods -n <your-namespace> -l app=<service-name> -o wide

# 3. ArgoCD app is synced and healthy
argocd app get <service-name> | grep -E "Status|Health|Sync Policy"

# 4. Service endpoint works
curl -s http://$(kubectl get service <service-name> -n <your-namespace> -o jsonpath='{.status.loadBalancer.ingress[0].ip}')/health | jq .

# 5. Git is the source of truth
echo "Next deployments will be: git push → ArgoCD auto-sync → cluster update"
```

Expected results:
- Deployment has label `managed-by=argocd`
- All pods running
- ArgoCD app synced and healthy
- Service endpoint responses with health check
- Team understands GitOps workflow is now active

---

## Rollback

If adoption needs to be rolled back to manual deployment:

```bash
# Delete ArgoCD Application
argocd app delete <service-name>

# This removes all resources ArgoCD created
# Redeploy manually if needed
kubectl apply -f deployment-backup.yaml
kubectl apply -f service-backup.yaml

# Verify manual deployment is running
kubectl get deployment <service-name> -n <your-namespace>
```

---

## Common Issues

| Error | Cause | Fix |
|---|---|---|
| Conflict: Resources already exist | Old and new deployments run simultaneously | Delete old deployment: `kubectl delete deployment <old-name> -n <namespace>` |
| OutOfSync status in ArgoCD | Git content differs from cluster | Run `argocd app sync <service-name>` or wait for auto-sync period |
| PermissionDenied sync errors | Project RBAC not configured | Ask DevOps: confirm Project includes your repo and namespace |
| Deployment stuck in old version | Image pull secret missing | Verify ACR secret created: `kubectl get secret -n <namespace>` |
| ArgoCD can't access Git repo | SSH key or HTTPS credentials missing | Ask DevOps: configure Git credentials in ArgoCD |

---

## Tips for Success

1. **Test in non-prod first** — Adopt ArgoCD in dev/staging before prod
2. **Use sync waves** — For multi-component services, control order with sync waves
3. **Enable notifications** — Set up ArgoCD notifications for sync failures
4. **Document your process** — Add steps to your team's onboarding guide
5. **Monitor first sync** — Watch logs closely during initial ArgoCD sync

---

## Related Artifacts

- Doc Gap: [DG-0001 — Namespace not pre-provisioned](../doc-gaps/docgap-dg-0001-argocd-namespace-not-preprovisioned.md)
- Doc Gap: [DG-0002 — Cluster not registered](../doc-gaps/docgap-dg-0002-argocd-cluster-not-registered.md)
- Doc Gap: [DG-0003 — RBAC not configured](../doc-gaps/docgap-dg-0003-argocd-project-rbac-not-configured.md)
- Runbook: [RBK-0004 — Platform onboarding quick steps](runbook-rbk-0004-platform-onboarding-quick-steps.md)
- Runbook: [RBK-0005 — Podman to AKS migration](runbook-rbk-0005-podman-to-aks-argocd-migration.md)
