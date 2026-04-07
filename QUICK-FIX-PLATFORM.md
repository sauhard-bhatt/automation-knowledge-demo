# Quick Fixes by Platform

**Copy the section for your platform. Copy the fix. Run. Done.**

---

## ArgoCD + AKS

### namespaces ".*" not found
```bash
kubectl create namespace <name>
argocd app sync <app-name>
```
Verify: `argocd app get <app-name> | grep Status`

---

### open values.*: no such file or directory
```bash
kubectl patch app <app-name> -n argocd --type merge \
  -p '{"spec":{"source":{"helm":{"valuesFiles":["values/dev.yaml"]}}}}'
argocd app sync <app-name>
```
Verify: `argocd app get <app-name> | grep Conditions`

---

### cluster ".*" not found
```bash
argocd cluster list
argocd cluster add <kube-context> --name <cluster-name>
# OR
kubectl patch app <app-name> -n argocd --type merge \
  -p '{"spec":{"destination":{"name":"<registered-cluster>"}}}'
argocd app sync <app-name>
```
Verify: `argocd app get <app-name> | grep Destination`

---

### forbidden: User.*cannot create resource
```bash
kubectl create namespace <target-namespace>
# OR
kubectl create clusterrole argocd-ns --verb=create --resource=namespaces
kubectl create clusterrolebinding argocd-ns \
  --clusterrole=argocd-ns \
  --serviceaccount=argocd:argocd-application-controller
argocd app sync <app-name>
```
Verify: `argocd app get <app-name> | grep Conditions`

---

### Sync failed: hook / Job ".*" failed
```bash
kubectl logs -n <namespace> job/<job-name>
# Fix root cause, then:
argocd app sync <app-name> --force
```
Verify: `kubectl get job -n <namespace> <job-name> && argocd app get <app-name> | grep Status`

---

## Azure App Service

### TargetInvocationException
```bash
az monitor app-insights query --app <app-insights-name> \
  --query "exceptions | where type == 'TargetInvocationException'" \
  --scope last_24h
az webapp log tail --name <app-name> --resource-group <rg-name>
az webapp restart --name <app-name> --resource-group <rg-name>
```
Verify: `az webapp show --name <app-name> --resource-group <rg-name> | grep -i "state"`

---

### 401 Unauthorized
Pending: See [indexes/error-signatures-by-platform.md](indexes/error-signatures-by-platform.md)

---

### 503 Service Unavailable
Pending: See [indexes/error-signatures-by-platform.md](indexes/error-signatures-by-platform.md)

---

## Azure Container Apps (ACA)

### Container failed to start
```bash
az containerapp logs show --name <app-name> --resource-group <rg-name>
az acr repository show --name <registry-name> --image <image-name>
az containerapp update --name <app-name> --resource-group <rg-name> \
  --image <correct-image>
```
Verify: `az containerapp show --name <app-name> --resource-group <rg-name> | grep -i "provisioning"`

---

### Environment variable not found
Pending: See [indexes/error-signatures-by-platform.md](indexes/error-signatures-by-platform.md)

---

### Port already in use
Pending: See [indexes/error-signatures-by-platform.md](indexes/error-signatures-by-platform.md)

---

## App Service on Podman

### Image pull failed
```bash
podman image ls | grep <image>
podman pull <registry>/<image>:<tag>
# If auth needed:
podman login <registry>
podman pull <registry>/<image>:<tag>
podman restart <container-id>
```
Verify: `podman image ls | grep <image>`

---

### Container runtime error
Pending: See [indexes/error-signatures-by-platform.md](indexes/error-signatures-by-platform.md)

---

### Volume mount denied
Pending: See [indexes/error-signatures-by-platform.md](indexes/error-signatures-by-platform.md)

---

## WebLogic

### ClassNotFoundException
```bash
tail -f $DOMAIN_HOME/servers/AdminServer/logs/AdminServer.log
ls -la $DOMAIN_HOME/lib/ | grep <jar-name>
# Add JAR if missing:
cp <jar-file> $DOMAIN_HOME/lib/
$DOMAIN_HOME/bin/stopWebLogic.sh
$DOMAIN_HOME/bin/startWebLogic.sh
```
Verify: `tail -f $DOMAIN_HOME/servers/AdminServer/logs/AdminServer.log | grep "Started"`

---

### Connection refused
Pending: See [indexes/error-signatures-by-platform.md](indexes/error-signatures-by-platform.md)

---

### OutOfMemoryError
Pending: See [indexes/error-signatures-by-platform.md](indexes/error-signatures-by-platform.md)

---

**For more platforms & errors: [indexes/by-platform.md](indexes/by-platform.md)**
