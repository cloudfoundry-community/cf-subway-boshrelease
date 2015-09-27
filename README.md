BOSH release for Subway
=======================

A subway to scale out Cloud Foundry Service Brokers.

```
________   ______________________>__
[]_[]||[| |]||[]_[]_[]|||[]_[]_[]||[|
===o-o==/_\==o-o======o-o======o-o==/______
:::::::::::::::::::::::::::::::::::::::::::
```

Subway is a multiplexing service broker that allows you to scale out single node brokers, such as cf-containers-broker/docker-boshrelease and cf-redis-broker/cf-redis-release.

-	Project https://github.com/cloudfoundry-community/cf-subway

Usage
-----

To use this bosh release, first upload it to your bosh:

```
bosh upload release https://bosh.io/d/github.com/cloudfoundry-community/cf-subway-boshrelease
```

For [bosh-lite](https://github.com/cloudfoundry/bosh-lite), you can quickly create a deployment manifest & deploy a node for a given set of backend brokers:

```
cat > tmp/my-brokers.yml <<-EOS
---
properties:
  subway_broker:
    backend_brokers:
    - https://warreng:natedogg@haash-broker-1.cfapps.io
    - https://warreng:natedogg@haash-broker-2.cfapps.io
    port: 8000
    username: secretusername
    password: secretpassword
EOS

templates/make_manifest warden tmp/my-brokers.yml
bosh -n deploy
```

Once deployed, the Subway broker can be registered with `secretusername` and `secretpassword` as its username/password (based on example above).

The default port is `8000`.
