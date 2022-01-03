---
category: post
title: Docker Containers
subtitle: Getting in depth of docker containers
background: '/img/home-bg.jpg'
---

## Docker container - TLDR  
A container is the runtime instance of an image. In the same way that you can start a virtual machine (VM) from a virtual machine template, you can start one or more containers from a single image. The big difference between a VM and a container is that containers are faster and more lightweight. Instead of running a full-blown OS like a VM, containers share the OS/kernel with the host they’re running on. It’s also common for containers to be based on minimalist images that only include software and dependencies required by the application.


### Starting a container  
Simplest way to run a container from docker image is  
`docker container run <image> <app>`

```sh
docker container run -it ubuntu /bin/bash
```

<img src="/gifs/docker_container_run.gif" alt="docker_container_run"
	title="docker container run" width="900" height="400" />

### Stopping a container  
Containers run until the app they are executing exits.  
In the above command, when bash shell exits the container stops. 

User can manually stop container as well `docker container stop`  
and restart it again with `docker container start`.  
To get rid of the container completely, run `docker container rm`  


## Containers vs VMs  
At a high level, *hypervisors* perform `hardware virtualization`. They carve up physical hardware resources into virtual versions called VMs.  
On the other hand, *containers* perform `OS virtualization`. They carve OS resources into virtual versions called containers.


### VM tax  
The VM model carves low-level hardware resources into VMs. Each VM is a software construct containing virtual CPUs, virtual RAM, and virtual disks, etc. As such, every VM needs its own OS to claim, initialize, and manage all of those virtual resources. And sadly, every OS comes with its own set of baggage and overheads. For example, every OS consumes a slice of CPU, a slice of RAM, and a slice of storage, etc. Some need their own licenses, as well as people and infrastructure to patch and upgrade them. Each OS also presents a sizable attack surface. We often refer to all of this as the OS tax or VM tax. Every OS you install consumes resources!


## Docker commands  

- `docker container run` is the command used to start new containers. In its simplest form, it accepts an image and a command as arguments. The image is used to create the container, and the command is the application the container will run when it starts. This example will start an Ubuntu container in the foreground and tell it to run the Bash shell: `docker container run -it ubuntu /bin/bash`.

- `Ctrl-PQ` will detach your shell from the terminal of a container and leave the container running `(UP)` in the background.

- `docker container ls` lists all containers in the running `(UP)` state. If you add the `-a` flag, you will also see containers in the stopped `(Exited)` state.

- `docker container exec` runs a new process inside of a running container. It’s useful for attaching the shell of your Docker host to a terminal inside of a running container. This command will start a new Bash shell inside of a running container and connect to it: `docker container exec -it <container-name or container-id> bash`. For this to work, the image used to create the container must include the Bash shell.

- `docker container stop` will stop a running container and put it in the `Exited (0)` state. It does this by issuing a `SIGTERM` to the process with PID 1 inside of the container. If the process has not cleaned up and stopped within 10 seconds, a SIGKILL will be issued to forcibly stop the container. `docker container stop` accepts container IDs and container names as arguments.

- `docker container start` will restart a stopped `(Exited)` container. You can give `docker container start` the name or ID of a container.

- `docker container rm` will delete a stopped container. You can specify containers by name or ID. It is recommended that you stop a container with the `docker container stop` command before deleting it with `docker container rm`.

- `docker container inspect` will show you detailed configuration and runtime information about a container. It accepts container names and container IDs as its main argument.



