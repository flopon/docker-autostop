# docker-autostop

Monitor and stop docker containers depending of a missing one. 

## How to use
```bash
docker run -d \
    --name autostop \
    --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    flopon/autostop
```
Apply the label `autostop.depends_on=<CONTAINER>` to your container to have it watched.
If the CONTAINER is not running on the current docker node, the monitored container will be stopped

## ENV Defaults
```
AUTOSTOP_CONTAINER_LABEL=autostop.depends_on # You can customize the reference label
AUTOSTOP_INTERVAL=5   # check every 5 seconds
AUTOSTOP_START_PERIOD=0   # wait 0 seconds before first health check
AUTOSTOP_DEFAULT_STOP_TIMEOUT=10   # Docker waits max 10 seconds (the Docker default) for a container to stop before killing during restarts (container overridable via label, see below)
DOCKER_SOCK=/var/run/docker.sock   # Unix socket for curl requests to Docker API
CURL_TIMEOUT=30     # --max-time seconds for curl requests to Docker API
```

### Optional Container Labels
```
autostop.timeout=20        # Per containers override for stop timeout seconds during restart
```
