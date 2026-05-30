# Build

```bash
cd package/server-ee
cd package/server-ce
make format
```

```
make server-ee
```

```
cd package/server-ee
make build-image -e ENV=production
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

```bash
docker push harbor.k8s.shubhamtatvamasi.com/portainer/portainer-ee:node-shell
```
