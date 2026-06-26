# Build

```bash
cd package/server-ee; make format; cd -
cd package/server-ce; make format; cd -
```

```
cd package/server-ee
PLATFORM=linux ARCH=amd64 make build-image -e ENV=production
cd -
```

```
docker tag \
  portainerci/portainer-ee:local \
  harbor.k8s.shubhamtatvamasi.com/portainer/portainer-ee:node-shell
docker push harbor.k8s.shubhamtatvamasi.com/portainer/portainer-ee:node-shell
```

```bash
kubectl rollout restart deployment portainer -n portainer
```

---


```
docker tag \
  portainerci/portainer-ee:local \
  harbor.k8s.shubhamtatvamasi.com/portainer/portainer-ee:new-custom-resources
docker push harbor.k8s.shubhamtatvamasi.com/portainer/portainer-ee:new-custom-resources
```

---

### OLD

```
make server-ee
```

```bash
docker buildx build \
  --no-cache --load \
  --platform linux/amd64 \
  --build-arg ENV=production \
  -t harbor.k8s.shubhamtatvamasi.com/portainer/portainer-ee:node-shell \
  -f /home/ubuntu/portainer-suite/package/server-ee/build/linux/Dockerfile \
  /home/ubuntu/portainer-suite/package/server-ee
```
