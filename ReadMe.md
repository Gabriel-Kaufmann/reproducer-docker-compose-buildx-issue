# Issue Reproducer
___
For docker-compose using build with buildkit/buildx enabled,
causing buildx not finding referenced images that are known by docker-host or 
that are provided during build.

## To start reproduction of error:
You may require either a local or remote docker-registry. I'm
not shure if buildx is able to push/pull from docker-host running buildx-container.
```
docker-compose build --push --pull
```

### After failing
You can check if your docker-host has the service-a image available:
```
docker image ls | grep 'registry.php-stack.docker/service'
registry.php-stack.docker/service-a     local       c0881693c02c   xx hours ago     7.34MB
```

---
#### Testing with local registry
To test locally you may roll-out docker-registry:v2 service. An example is provided here
by [docker-compose.local-registry.yml](docker-compose.local-registry.yml). You either must
configure docker.json and buildkit.toml to allow insecure/http registry or you must rollout
local mkcert to enshure ssl-trust.
