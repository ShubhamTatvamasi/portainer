# portainer

Add helm repo:
```bash
helm repo add portainer https://portainer.github.io/k8s/
```

Install portainer:
```bash
helm upgrade -i portainer portainer/portainer \
  --create-namespace \
  --namespace portainer \
  --set "image.repository=portainer/portainer-ee" \
  --set service.type=ClusterIP \
  --set ingress.enabled=true \
  --set ingress.ingressClassName=traefik \
  --set "ingress.hosts[0].host=portainer.k8s.shubhamtatvamasi.com" \
  --set "ingress.hosts[0].paths[0].path=/" \
  --set "ingress.tls[0].secretName=shubhamtatvamasi-tls" \
  --set "ingress.tls[0].hosts[0]=portainer.k8s.shubhamtatvamasi.com" \
  --set trusted_origins.enabled=true \
  --set "trusted_origins.domains=portainer.k8s.shubhamtatvamasi.com" \
  --set enterpriseEdition.enabled=true \
  --set tls.force=true \
  --set tls.existingSecret=shubhamtatvamasi-tls
```

---


### Git

```bash
git config user.email "shubham.tatvamasi@portainer.io"
```

---

http://localhost:9000

Run portainer:
```bash
docker run -d \
  -p 9000:9000 \
  --name portainer \
  --restart unless-stopped \
  -v "/var/run/docker.sock:/var/run/docker.sock" \
  portainer/portainer-ce
```

Remove portainer container:
```bash
docker rm -f portainer
```


---

Create nginx container:
```bash
docker run -d -p 80:80 --name nginx nginx:alpine
```

Remove nginx container:
```bash
docker rm -f nginx
```
