---
category: til
title: Docker Images
subtitle: Getting in depth of docker images
---

## Brief
A docker image contains enough of an operating system (OS), as well as all the code and dependencies to run whatever application it’s designed for. Docker images are like stopped containers. Think of **image** as *build-time* construct and **containers** as *runtime-construct*

<figure>
<img src="/assets/img/docker_image_container_relation.png" alt="docker_images"
title="docker image and container high level relation" width="800" height="400" />
</figure>

We use the docker container run and docker service create commands to start one or more containers from a single image. Once you’ve started a container from an image, the two constructs become dependent on each other, and you cannot delete the image until the last container using it has been stopped and destroyed. 


### Pulling the image - Getting the image from remote repository to local repository
```sh
docker image pull alpine:latest
docker image ls
```


## Image registries
Docker images are stored in a centralized location known as *Image Registry*.
Image Registry contain multiple image repositories.

Run the following command to check the default image registry
```sh
docker info
```


## Image naming and tagging

> docker image pull \<repository\>:\<tag\>
>
> e.g. docker image pull alpine:latest

Pulling alpine image pull the image that is tagged as **latest**. It is not necessary that the pulled image will actually be latest.
If a **\<tag\>** is not specified then it tries to pull image with tag **latest** and the command fails in case it is not found.


### Multiple tags
Single image can have multiple tags.
```sh 
# To pull all tags of an image
docker image pull -a alpine
```

*latest* tag is not guaranteed to point to the latest image.

## filtering `image ls` output
```sh 
docker image ls --filter <filter_name>=<value>
```  
- Use option `--filter` to filter some of the *image ls* output.
    > docker image ls --filter dangling=true  
    > docker image ls --filter=reference="*:latest"  

- Use option `--format` to format the output.
    > docker image ls --format "\{\{.Size\}\}"  
    > docker image ls --format "\{\{.Repository\}\}: \{\{.Tag\}\}: \{\{.Size\}\}"


## `docker search`
The `docker search` command lets you search Docker Hub from the CLI. This has limited value, as you can only pattern-match against strings in the “NAME” field.  
And you can even filter out the results

> docker search alpine  
> docker search alpine --filter "is-official=true"

---
**NOTE**  
Just remember by default, Docker will only display 25 lines of results.  
However, you can use the --limit flag to increase that to a maximum of 100.

---


## Images and Layers  
A Docker image is just a bunch of loosely-connected read-only layers with each layer comprising one or more files.  
Docker takes care of stacking these layers and representing them as a single unified object.  
It’s important to understand that as additional layers are added, the image is always the combination of all layers stacked in the order they were added.  
Let's say there are two layers in an image and each layer has 3 files, but the overall image will have 6 files, as it is a combination of both layers.   

<figure>
<img src="/assets/img/docker_images_layers.png"
    alt="docker image and layers"
    width="800" height="400" >
<figcaption>Docker image as read-only layers</figcaption>
</figure>


You can inspect the layers in an image using command  
`docker image inspect <image_name>`  
> Sample:  
> docker image inspect --format "\{\{ .RootFS \}\}" ubuntu_sshd:latest

---
<figure>
<img src="/assets/img/docker_layers.png"
    alt="docker image layers"
    width="800" height="300" >
<figcaption>Multiple layers in a Docker image</figcaption>
</figure>


---  

Note: Let's say a file exist in multiple layers of an image, then image will have the latest version of the file.


## Pulling Image by digest  
#### Problem with tag  
Using tags has a problem. **Tags are mutable!** This means it’s possible to accidentally tag an image with the wrong tag (name). Sometimes, it’s even possible to tag an image with the same tag as an existing but different image.  
This can cause problems!  

#### How image digests works
Docker 1.10 introduced a content-addressable storage model. As part of this model, all images get a cryptographic content hash.  
As the digest is a hash of the contents of the image, it’s impossible to change the contents of the image without creating a new unique digest.  
To put it another way, you cannot change the content of an image and keep the old digest.  
This means digests are immutable and provide a solution to the problem with tags.  

> docker image ls --digests alpine  
  

**Pulling image using it's digest**  
> docker pull gcc@sha256:084eaedf8e3c51f3db939ad7ed2b1455ff9ce4705845a014fb9fe5577b35c901  


## Multi-Architecture Images  
Docker and Docker Hub have a slick way of supporting multi-arch images.  
This means a single image tag can support linux, windows, x64, arm etc.  

#### Internal working
To support this facility Registry API provides following constructs:  
- Manifest lists: A list of architectures supported by a particular image tag.   
- Manifest: Contains image config and layer data.  

Theory: Assume you are running Docker on a Raspberry Pi (Linux running on ARM architecture). When you pull an image, your Docker client makes the relevant calls to the Docker Registry API exposed by Docker Hub. If a manifest list exists for the image, it will be parsed to see if an entry exists for Linux on ARM. If an ARM entry exists, the manifest for that image is retrieved and parsed for the crypto ID’s of the layers that make up the image. Each layer is then pulled from Docker Hub.  

**Docker manifest**: The docker manifest command lets you inspect the manifest list of any image on Docker Hub.   
> docker manifest inspect golang \| grep 'architecture\\|os'  


## Deleting docker image  
```sh
docker image rm <image_id>  
#To delete all images  
docker image rm $(docker image ls -q) -f
```



---  

## References
1. Educative - [Course by Nigel Poulton](https://www.educative.io/courses/beginners-guide-to-docker)


