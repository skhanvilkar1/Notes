- Docker ^^build^^ command
  collapsed:: true
	- `docker build` command builds Docker images from a Dockerfile and a "context"
	- A build's context is set of files located in specified **PATH** or **URL**
	- **URL** parameter can refer to three kinds of resources: Git repositories, pre-packaged tarball contexts and plain text files.
	- Git URLs accept context configuration in their fragment section, separated by a colon (:). The first part represents the reference that Git will check out, and can be either a branch, a tag, or a remote reference. The second part represents a subdirectory inside the repository that will be used as a build context.
	- For example, run this command to use a **directory called docker in the branch container**:
	- `$ docker build https://github.com/docker/rootfs.git#container:docker`
	- **Tarball contexts** `$ docker build https://server/context.tar.gz`
	- `$ docker build -f /home/myapp/dockerfiles/debug /home/myapp` // This command uses debug file as Dockerfile, note that we used -f option to make it possible and build context is /home/myapp
	- --build-arg : Setting build time variables. If your Dockerfile has ARG specified, you can use this option in command to change it during build time.
	- E.g. : `$ docker build --build-arg HTTP_PROXY=http://10.20.30.40:1234`
	-
	-
- How to ^^search^^ Image
  collapsed:: true
	- docker search httpd
	- docker search httpd --limit 2
	- docker search --filter stars=10 httpd
- Image addressing convention
  collapsed:: true
	- image: `httpd/httpd`
	-
- How to ^^pull^^ images
  collapsed:: true
	- `$ docker image pull <repository>:<tag>`
	- Pulling from 3rd party : `$ docker image pull gcr.io/google-containers/git-sync:v3.1.5`
- How to ^^save^^ and ^^load^^ images - When you cannot access docker hub online.
  collapsed:: true
	- Use _docker image [save]_ and _docker image [load]_ commands to save and load image files. On hosts with internet access download the images and use image save command to create tar file
		- `docker image save alpine:latest -o alpine.tar`
	- Use docker image load command to load on host with no internet access
		- `docker image load -i alpine.tar`
- How to convert container to images using ^^export^^
  collapsed:: true
	- `docker export <container-name> > testcontainer.tar`
- How to convert exported image tar files to normal images using ^^import^^
  collapsed:: true
	- `docker image import testcontainer.tar > newimage:latest `
	  This will extract the tar file to local image and image can be used to create containers.
- How to ^^search^^ for images in docker hub registry from commandline
  collapsed:: true
	- `docker image search --filter stars=2  --filter is-official=true httpd `
	- `docker search --limit=2 httpd`
- How to ^^push^^ docker images -
  collapsed:: true
	- Always tag with your username e.g. swapnil/image:tag before pushing
- [[Building a custom Image]]
  collapsed:: true
	- {{embed [[Building a custom Image]]}}
	-
- How to ^^commit^^ a container and create an image.
  collapsed:: true
	- `docker container commit -a "Ravi" httpd customhttpd` here -a is to mention name of author, httpd is container started and customhttpd is name of image created
	- **Dockerfile** is **recommended** approach , export is NOT recommended approach for production purposes.
	-
- What is a ^^Build Context^^
  collapsed:: true
	- Consider example of copying source code file to image here.
	- Docker Daemon should have access to files to build the image.
	- All files specified in Dockerfile is the build context and is transferred to Docker daemon (same host or different host as well) under the location /var/lib/docker/tmp/docker-builderxxx
	- Make sure files are minimum since transfer files can take time and will prolong the building time of image.
	- to ignore temporary files (not necessary for build) but are present in same directory, you can configure a `.dockerignore` and add list of files under this `.dockerignore` file. Referencing this list, those mentioned , will be ignored for the transfer to the daemon.
	- you can also refer a code repository (git url) to build images. e.g. `docker build https://github.com.swapnil/build`
	-
- What is a ^^Build Cache^^
  collapsed:: true
	- Docker first checks the instructions set. So if instruction is same, it will use cache
	- If docker file is modified, then cache for that layer is invalidated , along with cache for next layers as well and are rebuild.
	- What if I modify code, instruction is the same what will happen ? Docker also confirms the ^^checksum^^ of files in _ADD or COPY_. So if checksum is changed, cache is invalidated and cache is invalidated along with that for another layers.
	- what is version pinning ? read about it
- COPY vs ADD
  collapsed:: true
	- Look very similar copies files and directories from local system to docker image. But docker ADD command has extra features
	- with ADD you can specify path to a tar file and it will be extracted to image e.g. 
	  ```
	  Dockerfile
	  FROM centos:7
	  ADD app.tar.xz /testdir
	  ````
	- It is recommended to use COPY instruction whenever possible. ADD works differently with different options. To keep images small lean as much as possible.
- CMD vs ENTRYPOINT
  collapsed:: true
	- If you run a `docker run ubuntu` it runs and exists immediately
	- Unlike VMs containers are not meant to host OSs, they are meant to run processes. Once the task is complete the container exists. It only lives till the process is alive.
	- Who defines what Process runs in the container ?
	  `CMD` -> it has commands that run on the container. 
	  Make image from Base OS image and specify your own command. CMD is hard coded.
	- To invoke sleep command automatically use `ENTRYPOINT`.
	- Its like command instruction. `ENTRYPOINT ["sleep"]`
	  `docker run ubuntu-sleeper 10`
	- Ideal way to write, for both CMD and ENTRYPOINT to work together parameters should be in ^^JSON^^ format only
	- ````
	  FROM Ubuntu
	  ENTRYPOINT ["sleep"]
	  CMD ["5"]
	  ````
	- `ENTRYPOINT` is optional , CMD can be inherited from Base images and you might notknow about it.
	- `CMD` -> **provides defaults to executing container**
	- `CMD` is appended to the `ENTRYPOINT` but there can be only one `CMD` instruction in Dockerfile. If there are more than one then last one counts
	- `ENTRYPOINT` is not often overridden.
	- to override use --entrypoint option when running the container
- Base vs Parent Images
  collapsed:: true
	- What is scratch ? Scratch is top-most image. Its blank , dockers reserved image name. All base images start from here first.
	- Most OSs have base images build already. Incase you want to build yourself, you can start from scratch.
- Multi-Stage Builds
  collapsed:: true
	- Containerizing multiple file/directory based applications to a container. Traditionally application build would be happening on local servers and then be distributed. This could lead to issues with clean build when working with images and challenge with clean build.
	- Solution is to use Dockerfile and containerize the build process in docker image build itself.
	  ````
	  FROM node AS builder #stage 0
	  COPY . .
	  RUN npm install 
	  RUN npm run build 
	  
	  FROM nginx           #stage 1
	  COPY --from=builder dist /usr/share/ngnix/html #can also be written --from=0 which is stage no. 
	  CMD ["nginx", "-g", "daemon off;"]
	  ```
	-
	- Optimizes DockerFiles easy to read and maintain, low size, avoid multiple Dockerfiles and no intermediate images
- What is Docker ^^inspect^^ command.
- What are manifests and manifest lists?
  collapsed:: true
	- All official images have manifest list. Which image supports which architecture (CPU arch.) and platform? (OS). A docker command to check manifest `$ docker manifest inspect alpine | grep 'architecture \| os`
	- Docker images are hence independent of architecture as we feel it. But official images have manifest list which inturn have mainfest of supported layers from where its pulled.
	- You can even build your own image on your choice of architecture using **docker buildx** and then using **docker manifest create** commands.
	  E.g. `$ docker buildx build --platform linux/arm/v7 -t myimage:arm-v7 .`
	-