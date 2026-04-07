# Quick Troubleshooting (Precision Mode)

**Find your error below. Copy the fix command. Run. Done.**

---

## namespaces ".*" not found

**Fix:**
```bash
kubectl create namespace <name>
argocd app sync <app-name>
```

**Verify:**
```bash
argocd app get <app-name> | grep Status
```

---

## open values.*: no such file or directory

**Fix:**
```bash
# Verify path in Application
kubectl get app <app-name> -n argocd -o yaml | grep -A 3 helm:

# Update and sync
kubectl patch app <app-name> -n argocd --type merge \
  -p '{"spec":{"source":{"helm":{"valuesFiles":["values/dev.yaml"]}}}}'
argocd app sync <app-name>
```

**Verify:**
```bash
argocd app get <app-name> | grep Conditions
```

---

## cluster ".*" not found

**Fix:**
```bash
# Check registered clusters
argocd cluster list

# Register missing cluster
argocd cluster add <kube-context> --name <cluster-name>

# OR update Application destination
kubectl patch app <app-name> -n argocd --type merge \
  -p '{"spec":{"destination":{"name":"<registered-cluster>"}}}'

argocd app sync <app-name>
```

**Verify:**
```bash
argocd app get <app-name> | grep Destination
```

---

## forbidden: User.*cannot create resource

**Fix:**
```bash
# Option A: Create namespace first
kubectl create namespace <target-namespace>
argocd app sync <app-name>

# Option B: Grant permission
kubectl create clusterrole argocd-ns --verb=create --resource=namespaces
kubectl create clusterrolebinding argocd-ns \
  --clusterrole=argocd-ns \
  --serviceaccount=argocd:argocd-application-controller
argocd app sync <app-name>
```

**Verify:**
```bash
argocd app get <app-name> | grep Conditions
```

---

## Sync failed: hook / Job ".*" failed

**Fix:**
```bash
# Check job logs
kubectl logs -n <namespace> job/<job-name>

# Fix root cause, then retry
argocd app sync <app-name> --force
```

**Verify:**
```bash
kubectl get job -n <namespace> <job-name>
argocd app get <app-name> | grep Status
```

---

**For details: see [knowledge/incidents/](knowledge/incidents/)**
