# Enterprise Edition


```bash
helm upgrade -i portainer portainer/portainer \
  --create-namespace \
  --namespace portainer \
  --set enterpriseEdition.enabled=true \
  --set enterpriseEdition.image.repository=harbor.k8s.shubhamtatvamasi.com/portainer/portainer-ee \
  --set enterpriseEdition.image.tag=node-shell \
  --set trusted_origins.enabled=true \
  --set trusted_origins.domains=https://portainer.k8s.shubhamtatvamasi.com \
  --set service.type=ClusterIP \
  --set ingress.enabled=true \
  --set ingress.ingressClassName=traefik \
  --set "ingress.hosts[0].host=portainer.k8s.shubhamtatvamasi.com" \
  --set "ingress.hosts[0].paths[0].path=/" \
  --set "ingress.tls[0].secretName=shubhamtatvamasi-tls" \
  --set "ingress.tls[0].hosts[0]=portainer.k8s.shubhamtatvamasi.com" \
  --set tls.existingSecret=shubhamtatvamasi-tls \
  --set 'persistence.annotations.helm\.sh/resource-policy=keep'
```


```bash
kubectl -n portainer patch deployment portainer \
  --type='json' \
  -p='[
    {
      "op": "replace",
      "path": "/spec/template/spec/containers/0/args",
      "value": [
        "--tlscert=/certs/tls.crt",
        "--tlskey=/certs/tls.key",
        "--trusted-origins=https://portainer.k8s.shubhamtatvamasi.com",
        "--no-csp"
      ]
    }
  ]'
```

```
kubectl -n portainer patch deployment portainer \
  --type='json' \
  -p='[
    {
      "op": "replace",
      "path": "/spec/template/spec/containers/0/args",
      "value": [
        "--tlscert=/certs/tls.crt",
        "--tlskey=/certs/tls.key",
        "--trusted-origins=https://portainer.k8s.shubhamtatvamasi.com",
        "--node-shell"
      ]
    }
  ]'
```


