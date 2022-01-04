---
category: til
title: Dockerfile
subtitle: Dockerfile
---

## Sample Dockerfile  
```
FROM alpine  
LABEL maintainer="example@gmail.com"  
RUN apk add --update nodejs nodejs-npm  
COPY . /src  
WORKDIR /src  
RUN npm install  
EXPOSE 8080  
ENTRYPOINT ["node", "./app.js"]  
```

## Details  
- FROM: The base layer of the image.  
- LABEL: Simple key-value pairs and are an excellent way of adding custom metadata to an image.  
- RUN: Uses `apk` package manager to create a layer on top of base layer and installs packages on it.  
- COPY: The COPY . /src instruction creates another new layer and copies in the application and dependency files from the *build context*.  
- WORKDIR: Set the working directory inside the image filesystem for the rest of the instructions in the file.  
- RUN: RUN npm install instruction creates a new layer and uses npm to install application dependencies listed in the package.json file in the build context.  
- EXPOSE: The application exposes a web service on TCP port 8080, so the Dockerfile documents this with the EXPOSE 8080 instruction.  
- ENTRYPOINT: The ENTRYPOINT instruction is used to set the main application that the image (container) should run.  

<figure>
<img src="/assets/img/docker_custom_image_layers.png" alt="docker_custom_image_layers"
title="docker custom image layers" width="800" height="400" />
</figure>


## Pushing to docker registry - TL;DR  
- docker image build -t web:latest .  
- docker login
- docker image tag web:latest \{\{username\}\}/web:latest  
- docker image push \{\{username\}\}/web:latest  
- docker container run -d --name c1 -p 8000:8080 web:latest  


