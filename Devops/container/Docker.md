---
date updated: '2021-08-21T22:05:22+07:00'

---

# Docker

## Common Command

### Network

#### Create network

```shell
docker network create <network-name>
```

### Images

#### Build image

```shell
docker build -t <image-tag> <path-to-image>
```

Adđing `no-cache` parameter to build iamge without using cache

#### Listing image

```shell
docker images
```

#### Deleting image

```shell
docker rmi <image-id>
```

#### Pulling image

```shell
docker pull <image-tag>
```

#### Publishing image

```shell
docker image tag rhel-httpd:latest registry-host:5000/myadmin/rhel-httpd:latest

docker image push registry-host:5000/myadmin/rhel-httpd:latest
```

### Exporting image

```shell
docker image save <image-id> -o output.tar
```

### Loading image

```shell
docker image load <input-file>
```


### Container

#### Listing container

```shell
docker ps
```

The above command will listing all runiing container. To list all container including idle container,  run
```shell
docker ps -a
```

#### Running container

```shell
docker run -p 80:80 nginx
```

#### Executing container

```shell
docker exec -it <container-name> /bin.sh
```

#### Inspecting containter log

```shell
docker logs -f <container-id>
```

### Cleaning

#### Killing all container
```shell
docker kill $(docekr ps -q )
```

#### Pruning

```shell
docker system prune
```

Tags: #docker, #devops 