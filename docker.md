containerization technology
easy for developer to produce the container image
comparing containers to vm - sort of like a vm run on the server, server shares same desktop writing kernel, speed benefits
containers and vms can live together
docker community edition and enterprise edition
docker store - docker community (don't use docker toolbox)

##Terminology
* Images - the file system and configuration of your application which are used to create containers; images are pulled from the Docker Registry by default
* Containers - running instances of Docker images; containers run the actual applications. A container includes an application and all of its dependencies. It shares the kernel with other containers, and runs in an isolated process in user space and on the host OS.
* Docker _daemon_ - the background service running on the host that manages building, running, and distributing Docker containers
* Docker client - the command line tool that allows the user to interact with the Docker daemon
* Docker Store - Store is a registry of Docker images: a directory of all available Docker images

##Commands
`docker container ls` shows a list of running containers
`docker ls image` lists your docker images
`docker run` creates a container
`docker image pull`
`docker image inspect`


