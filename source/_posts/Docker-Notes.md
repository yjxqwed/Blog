---
title: Docker Notes
date: 2020-12-09 18:12:39
tags:
---

This post is to archive some commonly used docker commands.

## Build
### Command
Build an image.
```bash
# build
$ docker build [OPTIONS] PATH

# examples
$ docker build -t test:0.1 .
$ docker build -t test:0.1 -f ./Dockerfile1 .
```

### Dockerfile
Dockerfile is the 'script' to build the image.
```dockerfile
# Indicate an image based on which to build the image.
FROM <base-image>

# Indicate the workdir in the image to operate further operations
WORKDIR <workdir>

# Copy files from host into the image
# <host_path> is absolute or relative to the PATH specified in the 'docker build' command
# <image_path> is absolute or relative to <workdir>
COPY <host_path> <image_path>

# Run some commands (shell styled), usually to install softwares.
# For better performance, run multiple commands using a single RUN.
RUN <cmd> [&& <cmd>]
```

## Run
Run an image
```bash
$ docker run -dit --net=host --restart=always --privileged \
    --name=<container_name> \
    -v <host_path>:<container_path>
```
`--net=host` Automatically map all ports.  
`--restart=always` Restart the container when docker restarts.  
`-v <host_path>:<container_path>` Bind mount a volume. You can bind your code dir to a container and build your code inside a container!

## Exec
Execuate some command upon a container, usualy a shell.
```bash
$ docker exec -it <container> bash
```

## Miscellaneous
```bash
# stop a container
$ docker stop <container>

# restart a container
$ docker restart <container>

# list running containers
$ docker ps

# list containers
$ docker container ls

# list local images
$ docker image ls
$ docker images

# remove a container
$ docker container rm <container>

# remove an image
$ docker image rm <image>

# get info of a container
$ docker inspect <container>
```
