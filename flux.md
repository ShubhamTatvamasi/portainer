# flux

Delete portainer:
```bash
kubectl delete kustomizations portainer -n flux-system
```

Redeploy portainer:
```bash
flux-operator reconcile rset infrastructure -n flux-system
```
