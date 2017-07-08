Getting Started with Docker
### Docker for Mac
* Runs a VM with Linux and exposes Docker Engine on the Linux VM back to your Mac
* Uses Hyperkit (DataKit, Moby Linux VM) to implement a super light weight hypervisor
* Works only with Linux-based Docker containers

### Working with Containers
* Hypervisors use physical resources (CPU, RAM, storage, networks) and slices them into virtual versions and slices them into VMs
* Hypervisors virtualize physical server resources and builds virtual machines
* Container engines like Docker are more like operating system virtualization - create virtual OSs that are assigned to each container; much more lightweight than VMs
* Docker and other container engines use OS resources (process namespace, network stack, file system hierarcy)
* Every container gets its own PID1, process ID 1 and root file system /

```bash
docker version # client and server info
docker info 
docker run <image> # to run a new container, -d (start container in detached mode, start in background and don't latch on to terminal), --name a unique name, -p 80:8080 map network ports (map port 80 on the docker host to port 8080 inside the container, docker host's publicly accessible DNS name), -it interactive terminal , /bin/bash shell access into container (containers are bare bones - single process constructs, don't want to be sshing into them and doing management stuff) 
ps -elf
top
docker ps # to see running and stopped containers
docker ps -a # show previous containers run
docker image # see info about images stored in local registry/image store (repository like image name, tag for versioning, image id - each image gets its own unique hash, 
docker pull <image> # pulls image to Docker Host/local registry without starting container
docker rmi <image> # remove image from Docker Host/local registry
docker start <container>
docker stop <container>
docker rm <container> # -f to force removal
ctrl P + Q # exit container without killing it
docker stop $(docker ps -aq) # -aq gets all docker container ids
docker rmi $(docker rmi -q) # remove all images
```

Docker host runs the Docker client and Docker daemon (often refered to as Docker engine or sometimes just daemon)
Install Docker gives you the client and the daemon
Client makes API calls to the daemon
Daemon implements the Docker Remote API (Docker Engine API)
`docker run` starts a new container and we specify the image we want to use as the template for the container
Daemon checks local store to see if it has a copy locally. If no, it search Docker hub (https://hub.docker.com), docker image registry (place to store image), default registry (docker trusted registry is a private registry)
The daemon pulls images it doesn't already have locally

### Containers and Images
* Images ~ Stopped containers
* Containers ~ Running images
* hashes corresponds to image layer being pulled

### Container Life Cycle
* Containers can be started, stopped, restarted ad infinitum (like VMs)
* Stopped containers come back with all data intact; only removed containers loss data
* top-level images are official images stored in the root of the Hub (second-level repos jessiedaubner/<repo>)

### Swarm Mode and Microservices
* True native clustering (1.12 and later), native clustering is a called a swarm
* a cluster = swarm
* engines in a swarm run in swarm mode
* manager nodes maintain 
* swarm mode is optional the swarm - High availability - recommended 3 or 5
* workers execute tasks
* only one is leader
* Raft consensus algorithm
* services - scalable and declarative
