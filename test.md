# Test

https://hub.docker.com/r/portainerci/portainer-ee/tags?name=pr-3800

Deploy Portainer in test environment:
```bash
kubectl apply -f portainer-test.yaml
```

Update the deployment image:
```bash
kubectl -n portainer set image deployment/portainer-test \
  portainer=shubhamtatvamasi/portainer-ee:gpu-metrics
```

https://localhost:9443

```
kubectl port-forward -n portainer deploy/portainer-test 9443:9443
```

Restart portainer-test:
```bash
kubectl rollout restart deployment portainer-test -n portainer
```
