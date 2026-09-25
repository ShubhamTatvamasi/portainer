# flux

Delete portainer:
```bash
kubectl delete kustomizations portainer -n flux-system
```

Verify:
```bash
kubectl ns portainer
```

Redeploy portainer:
```bash
flux-operator reconcile rset infrastructure -n flux-system
```
