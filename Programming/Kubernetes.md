# Docker and Kubernetes

## Kubernetes

- Get deployments

  ```bash
  kubectl get deployments [-n <namespace>]
  ```

- `"Unhandled Error" err="couldn't get current server API group list: the server has asked for the client to provide credentials"`
  ```bash
  systemctl restart k3s
  ```

## K3S

- Prune unused images

```bash
crictl rmi --prune
```

- Uninstall K3S

```bash
/usr/local/bin/k3s-uninstall.sh
```

## Docker Commands

- Build: `docker build [--no-cache] -t <username>/<repository> <path>`
- Push: `docker push <image_name>`
- Status: `docker ps`, `docker stats`
- Check Volumes: `docker volume ls`
- Remove Volume: `docker volume rm <volume>`

### Remove Unused Resources

Remove all unused resources, including volumes, except for containers and volumes associated with Docker Compose (even if the Compose file has been removed):

```bash
docker system prune -f -a --volumes
```

### Delete All Resources

1. Stop all containers:

```bash
docker stop $(docker ps -aq)
```

2. Delete all containers:

```bash
docker rm $(docker ps -aq)
```

3. Delete all images:

```bash
docker rmi $(docker images -aq)
```

4. Delete all volumes:

```bash
docker volume rm $(docker volume ls -q)
```

## Installation

### Debian

[Install Docker Engine on Debian](https://docs.docker.com/engine/install/debian/)

## Docker Compose

### Docker Compose Commands

- Start: `docker compose up [-d]`

- Stop: `docker compose down`

- Build: `docker compose build`

- Push: `docker compose push`

- Pull: `docker compose pull`

- Logs: `docker compose logs [-f] [service_name]`

- Stop containers, networks, and volumes: `docker compose down --volumes`

## Troubleshooting

1. Endless loading: Add a host entry for `http.docker.internal` linked to the local machine IP.