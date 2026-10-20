# Build

format the code:
```bash
cd package/server-ee; make format; cd -
cd package/server-ce; make format; cd -
```

Build server docker image:
```
cd package/server-ee
PLATFORM=linux ARCH=amd64 make build-image -e ENV=production
cd -
```

Build agent docker image:
```bash
cd package/agent
PLATFORM=linux ARCH=amd64 make agent -e ENV=production
cd -
```

Public image:
```
docker tag \
  portainerci/portainer-ee:local \
  shubhamtatvamasi/portainer-ee:gpu-metrics
docker push shubhamtatvamasi/portainer-ee:gpu-metrics
```

Restart portainer:
```bash
kubectl rollout restart deployment portainer -n portainer
```

---

Private image:
```
docker tag \
  portainerci/portainer-ee:local \
  harbor.k8s.shubhamtatvamasi.com/portainer/portainer-ee:gpu-metrics
docker push harbor.k8s.shubhamtatvamasi.com/portainer/portainer-ee:gpu-metrics
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
