# API

### Start Portainer:

```bash
PORTAINER_VERSION=2.43.0
PORTAINER_USERNAME=admin
PORTAINER_PASSWORD=YourPassword!
docker run --rm -it \
  --name portainer \
  -p 9443:9443 \
  portainer/portainer-ee:${PORTAINER_VERSION} \
  --no-setup-token \
  --admin-password="$(docker run \
    --rm \
    httpd:alpine \
    htpasswd -nbB \
    ${PORTAINER_USERNAME} \
    ${PORTAINER_PASSWORD} \
    | cut -d: -f2)"
```

https://localhost:9443

---

### Access Portainer Via API

Authenticate as the admin account created by `--admin-password`:
```
JWT=$(curl -sk -X POST https://localhost:9443/api/auth \
  -H "Content-Type: application/json" \
  -d '{"Username":"admin","Password":"YourPassword!"}' | \
  python3 -c "import sys,json;print(json.load(sys.stdin)['jwt'])")
```

Check JWT Token:
```
echo $JWT
```

Confirm license state:
```
curl -sk https://localhost:9443/api/licenses/info -H "Authorization: Bearer $JWT"
```

Check System status:
```
curl -sk https://localhost:9443/api/system/status -H "Authorization: Bearer $JWT"
```

List endpoints (environments):
```
curl -sk https://localhost:9443/api/endpoints -H "Authorization: Bearer $JWT"
```

List teams:
```
curl -sk https://localhost:9443/api/teams -H "Authorization: Bearer $JWT"
```

Create a team (RBAC, EE feature):
```
curl -sk -X POST https://localhost:9443/api/teams \
  -H "Authorization: Bearer $JWT" -H "Content-Type: application/json" \
  -d '{"Name":"test-team"}'
```

List registries:
```
curl -sk https://localhost:9443/api/registries -H "Authorization: Bearer $JWT"
```

Create a registry:
```bash
curl -sk -X POST https://localhost:9443/api/registries \
  -H "Authorization: Bearer $JWT" \
  -H "Content-Type: application/json" \
  -d '{
    "Name": "harbor-shubhamtatvamasi",
    "Type": 3,
    "URL": "harbor.k8s.shubhamtatvamasi.com",
    "Authentication": true,
    "Username": "admin",
    "Password": "admin"
  }'
```

Full backup export:
```bash
curl -sk -X POST https://localhost:9443/api/backup \
  -H "Authorization: Bearer $JWT" -H "Content-Type: application/json" \
  -d '{}' -o backup.tar.gz
```

Extract backup:
```bash
tar -xzvf backup.tar.gz
```


