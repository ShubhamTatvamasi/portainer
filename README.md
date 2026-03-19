# portainer

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

Stop container:
```bash
docker rm -f portainer
```
