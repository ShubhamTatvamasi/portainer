# Edge

### Local Kubernetes

Name | rke2-edge
---|---
Portainer API server URL | https://portainer:9443
Portainer tunnel server address | portainer:8000


Check connection from kubernetes edge agent: 
```bash
kubectl run portainer-connectivity-check \
  --rm --attach --restart=Never \
  --image=portainer/agent:2.43.0 \
  --env="EDGE_CONNECTIVITY_CHECK=1" \
  --env="EDGE_CONNECTIVITY_CHECK_URL=https://portainer:9443" \
  --env="EDGE_INSECURE_POLL=1" \
  --env="EDGE_CONNECTIVITY_CHECK_TUNNEL_ADDR=portainer:8000"
```

---

### Remote Docker

Name | docker-edge
---|---
Portainer API server URL | https://portainer.k8s.shubhamtatvamasi.com
Portainer tunnel server address | https://edge-portainer.k8s.shubhamtatvamasi.com

Check connection from docker edge agent:
```bash
docker run --rm \
  -e EDGE_CONNECTIVITY_CHECK=1 \
  -e EDGE_CONNECTIVITY_CHECK_URL=https://portainer.k8s.shubhamtatvamasi.com \
  -e EDGE_INSECURE_POLL=1 \
  -e EDGE_CONNECTIVITY_CHECK_TUNNEL_ADDR=https://edge-portainer.k8s.shubhamtatvamasi.com \
  portainer/agent:2.43.0
```

---

Public k8s test:
```bash
kubectl run portainer-connectivity-check \
  --rm --attach --restart=Never \
  --image=portainerci/agent:pr-3800 \
  --env="EDGE_CONNECTIVITY_CHECK=1" \
  --env="EDGE_CONNECTIVITY_CHECK_URL=https://portainer.droplet.shubhamtatvamasi.com" \
  --env="EDGE_INSECURE_POLL=1" \
  --env="EDGE_CONNECTIVITY_CHECK_TUNNEL_ADDR=https://edge-portainer.droplet.shubhamtatvamasi.com"
```


---

```bash
curl -s https://downloads.portainer.io/ee2-45/portainer-edge-agent-setup.sh \
| sed 's|kubectl apply -f portainer-agent-edge-k8s.yaml|sed "s#image: portainer/agent:.*#image: portainerci/agent:pr-3800#" portainer-agent-edge-k8s.yaml > portainer-agent-edge-k8s-pr.yaml \&\& kubectl apply -f portainer-agent-edge-k8s-pr.yaml|' \
| bash -s -- 
```


