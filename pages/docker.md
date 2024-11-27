# installation
## docker engine
https://docs.docker.com/engine/install/ubuntu/
## docker compose

## desktop app
https://docs.docker.com/desktop/setup/install/linux/debian/
# docker commands
commands might be run as root user.

## pull and run an image
### pull
```sh
docker pull hello-world
```
### list images
```sh
docker images
```
### run the image
```sh
docker run hello-world
```
run with the terminal
```sh
docker run -it --name hello hello-world
```
run as a detached process
```sh
docker run --name my-nginx -d -p 80:80 nginx:latest
```
### list running containers
```
docker ps -a
```
### display container logs by their generated name
```sh
docker logs -t <container_name>
```
`-t` includes time.
### enter to a running terminal
```
docker exec -it my-nginx /bin/sh
```
### stop a container
you might stop a container before editing it.
```
docker stop <container_id>
```
### delete container by their id
```sh
docker rm <container_id>
```
image still exist.
### delete image
```sh
docker rmi hello-world:latest
```
## volumes
[volume documentation](https://docs.docker.com/engine/storage/volumes/)
### create volume
```sh
docker volume create my-vol
docker volume ls
```
### delete volume
```sh
docker volume rm my-vol
```
### start a container with a volume
```sh
```console
docker run -d \
  --name devtest \
  --mount source=myvol2,target=/app \
  nginx:latest
```
if the volume does not exist, Docker creates it for you. 
# dockerfile
[dockerfile docs](https://docs.docker.com/reference/dockerfile)
```Dockerfile
FROM debian:latest

```
# docker build
[docker build docs](https://docs.docker.com/reference/cli/docker/buildx/build/)
need a `Dockerfile` to be executed.
## commands
```sh
docker buildx build .
```
## options
```sh
--add-host
```
name and tag
```sh
-t <image_name>:<tag>
```
## useful tools
### [dive](https://github.com/wagoodman/dive)
A tool for exploring a docker image, layer contents, and discovering ways to shrink the size of your Docker/OCI image.
```sh
dive <my_container>:<version>
```
# docker compose
## install
it is generally installed with docker engine.
if not the case check the [installation instructions](https://docs.docker.com/compose/install/standalone/).
## commands
### run compose
```sh
docker compose up -d
docker compose stop # stop
docker compose down # stop and remove containers, networks and volumes
```
### run only one service
```sh
docker compose up <some_service>
```
### ps composes only
```sh
docker compose ps
```
### execute command to a running container
```sh
docker compose exec [OPTIONS] SERVICE COMMAND [ARGS...]
```
## docker-compose.yml
```yml
name: myapp

services:
  foo:
    image: busybox # locally built images can be used.
    command: echo "I'm running ${COMPOSE_PROJECT_NAME}"

```
### volume
```yaml
services:
  frontend:
    image: node:lts
    volumes:
      - myapp:/home/node/app
volumes:
  myapp:
```
# docker inspect
Return low-level information on Docker objects
```sh
docker inspec <container_id>
```
Get the container's ip
```sh
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <container_id>
```
