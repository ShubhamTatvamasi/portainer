# portainer

http://localhost:9000

Run portainer:
```bash
docker run -d -p 9000:9000 --name portainer \
  -v "/var/run/docker.sock:/var/run/docker.sock" \
  portainer/portainer
```

Stop container:
```bash
docker rm -f portainer
```
