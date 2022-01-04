---
category: til
title: Docker Technology
subtitle: Basic understanding of docker technology
---

# Major components:
1. The runtime
>The runtime operates at the lowest level and is responsible for starting and stopping containers (this includes building all of the OS constructs, such as [namespaces](https://man7.org/linux/man-pages/man7/namespaces.7.html) and cgroups).

    - **runc** -> low level runtime (one per running container). Interface with the underlying OS and start and stop containers
    - **containerd** -> high level runtime. talks to runc instances. It manages the entire lifecycle of a container, including pulling images, creating network interfaces, and managing lower-level runc instances.

2. The daemon (a.k.a. engine)
    - **dockerd** -> The Docker daemon (dockerd) sits above containerd and performs higher-level tasks, such as exposing the Docker remote API, managing images, managing volumes, managing networks, and more.

3. The orchestrator
    - **Docker swarm** -> Docker also has native support for managing clusters of nodes running Docker. These clusters are called “swarms” and the native technology is called “Docker Swarm.” Most people are choosing to use Kubernetes instead of Docker Swarm.

> docker daemon(engine) - implements the runtime, API, and everything else required to run Docker.
> 
> docker client 


## Docker Image
A docker image contains enough of an operating system (OS), as well as all the code and dependencies to run whatever application it’s designed for.

```sh
docker image pull ubuntu:latest
docker image ls
```
<!--
![Output](/assets/gifs/docker_images.gif){ width=90% height=30 style="float:left; padding:16px"}
-->

<img src="/assets/gifs/docker_images.gif" alt="docker_images"
	title="Output" width="900" height="400" />

## Building docker image

<img src="/assets/gifs/docker_pswebapp_image_build.gif" alt="build_docker_image"
	title="Output" width="1000" height="700" />

## Docker Container

```sh
docker container run -it ubuntu:latest /bin/bash
docker container ls
```

## Docker engine architecture
<img src="/assets/img/docker_engine_architecture.png" alt="docker_engine"
	title="Output" width="900" height="400" />


## References
Educative - [Course by Nigel Poulton](https://www.educative.io/courses/beginners-guide-to-docker)
