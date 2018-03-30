# Subway Deployment

```plain
bosh deploy manifests/cf-subway.yml \
  --vars-store tmp/creds.yml \
  -v backend-deployment=docker-broker \
  -v backend-broker=docker
```
