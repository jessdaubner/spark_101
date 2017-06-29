# Docker and Containers: The Big Picture

## What are Containers?
### Bad Old Days of physical servers
Applications run businesses
Applications run on servers
* Procurement lead times
* Up-front capex
* Ongoing capex

### VMWare / Virtualization Technology / Hypervisor Virtualization 
More efficient that physical servers
VMWare is a type of hypervisor
* Hypervisors allow multiple applications per server
* instead of one physical server for one app, one server could run multiple apps
* no longer automatic purchase of new server for new applications; only when really need themkkkkkjjjjkkk:17
* solved problem of wasting physical server resource
### Trouble with Hypervisors
* Virtual machines or virtual servers enable multiple applications to run on one server
* VMs are slices of the physical servers hardware (CPU, disk space, RAM)
* Each VM requires an OS which uses CPU, RAM, disk and may have license costs (resource and budget costs, operational baggage to manage)

### Containers 
* More efficient than hypervisor virtualization
* Virtualization 2.0
* Do not require VM or separate OS installation to launch application
* Less overhead since uses same OS as the server
* More free RAM/Disk/CPU available on the server
* Apps can be spun up quickly
* Less mature than hypervisor virtualization and less mature than hypervisor ecosystem
* Hypervisors will be around for a while, but containers are the future

Image: a stopped or powered off container; like a virtual machine template or OVF
* an image contains a container with an application
* each container has a unique ID

## What is Docker?
* Docker host: a server, most likely Linux, with the Docker engine installed

### Docker Inc
* Docker is to containers what VMware is to hypervisors
* Major sponsor and guardian of Docker project
* Docker Inc is behind Docker, based in SF, started off as dotCloud (selling developer platform paas, on top of AWS), Docker started off as an interal project

### Docker Project
* Docker is open-source, it is a community project
* Build, ship, and deploy better
* More than just the Docker engine
* Docker engine: core technology that other Docker projects and third-party tooling builds around; builds and manages images and starts and stops containers; main daemon
* Clustering, orchestration, registry, security are all build around the engine and plug into it
* Core components are written in Go/Golang (modern programming language that came out of Google)
* Aims for major point release every two months
* Docker Hub: public docker registry, place to store and retrieve images; public and private, third-party registries

### Open Container Initiative (OCI)
* Lightweight governance concil
* Standardize container runtime and format 
* Vendor and platform neutral
* Formed in June 2015 and run by CoreOS and Docker Inc
* Operates under Linux Foundation

## Preparing to Thrive in a Container World 
* Accept that containers are coming
* Introduce into CI/CD workflow (popular place to get developers started with containers)
* Start with distributed infrastructure
* Containers are not just for developers - operational IT/DevOps matters
* Orchestrations tools, clustering tools, mangement tools, monitoring and logging tools

## What Kind of Work Will Containers Do?
* Can containers be used for stateful applications (i.e., applications that persist data)?
* Docker can handled both stateless and stateful services but excels at stateless
* It is common to have both
### Stateful vs. Stateless 
#### Stateless
* Stateless app or service does not keep any data, forgets what it has just done after completion and moves onto the next job; does not keep any changes or the data (e.g., web servers that deliver static content) 
* Hypervisor virtualization allowed apps built on physical machines to easily be dropped onto virtual machines (could still use legacy apps)
* Legacy apps could be deployed in directly in containers but it is not as simple as with virtual machines
* We want to develop modern, microservice, scalable, self-healing, portable apps as the way forward, where we build the overall apps out of multiple small parts, can be deployed across multiple infrastructures and multiple cloudsjkjj
* Containers provide opportunity to rethink and redo apps
* Containers are great at modern cloud-native, microservices-style apps; far superior to virtual machines here
#### Stateful
* Stateful app or service remembers what it has done before; keeps changes and data (e.g., database or key-value store -- need to know what is already stored in db)
* Docker can be used for traditional, monolithic, stateful apps
* Databases can be used in Docker
* Docker containers are persistent by nature
....* stopping a container does not wipe its data
....* restarting a container brings back its data
....* container data stored in volumes persists even after the container is destroyed 
....* docker storage backend is pluggable (lots of plugins supporting portability of stateful containers and their data) 
....* stateful workloads are becoming first-class citizens 
* Pluggable storage backend is driving stateful workflows toward becoming first-class citizens in the Docker ecosystem

## DockerHub and Other Container Registries
* Centralized places to store and retreive images 
* Becoming the app store of enterprise IT
* Central to Docker experience
* Technically called image registries
* Just need an Internet connection and a new docker host can download any image
* DockerHub is the official registry but 3rd party registries exist
* Enable uploading and downloading of custom images to repositories
* Registries contain repositories

### Security
* Repositories can be public or private (public means other users can pull but not push to the repo)
* Containers are pulled from and pushed to registries 
* Private registries are available and run inside your corporate network (e.g. firewall or AWS VPC): Docker Trusted Registry (DTR), Quay Enterprise, etc.
* Container registries are becoming central to application infrastructure and application delivery

### Automated Workflow
* Development -> Github Repository -> Testing (automated unit tests) -> Container Registry (performs automated build producing updated container image to deploy from) -> Deployment
* Continuous Integration (CI) and Continuous Deployment (CD) 
* Containers registries are becoming central to app delivery 

## Are Docker and Containers Ready for Production and the Enterprise? 
### Docker Engine (build)
* Version 1.10 or higher
* Three channels: experimental (nighly releases, bleeding edge), stable (releases ~ every 2 months), commerically supported (~ 6 months, stable configs, support contract)

### Docker Swarm (build) 
* Native Docker clustering, sits on top of multiple Docker engines
* Already stable

### Docker Content Trust
* Enables users to verify both the publisher and content of images
* Authenticate content
* turns on image signing and verification for pushing and pulling images

Docker Hub (ship to the cloud)
Project Nautilus - scans images and detects known vunerabilities
Tutum, Docker Inc platform for deploying and managing apps in the cloud (run); can be used to deploy across multiple clouds
Docker Trusted Registry (DTR) - shipping for on-prem apps
Docker Universal Control Plane - on premise or in the cloud, Active Directory or LDAP integration for the enterprise (must haves for enterprise)
Also, Docker Machine and Docker Compose

Container ecosystem is growing rapidly outside of Docker Inc

## Container Orchestration
* Apps will likely contain multiple containers, microservices, hosts and even cloud infrastructures
* One app or app component may map one-to-one to a container
* Orchestration automates deployment and scaling (orchestration shines at scale to make overhead of setting it up worth it)
* How do all the different components (Load Balancer, Auth, HTTPs, Search, Log, DB) of the app fit together
* Do not want to manually specifiy which containers run on which hosts; specify a pool of hosts instead
* Define the app, provision the infrastructure and then deploy the app, scales the app (manages app dependencies and provides reproducible pattern)
* Docker orchestration products:
1. Docker Machine - Provisions docker hosts/images
2. Docker Compose - Compose multi-container apps, which images to use, networks ports to open, configuration settings to build app containers
3. Docker Swarm - Schedule containers over multiple Docker engine
4. Tutum - UI to control and manage
Ecosystem orchestration products: Kubernetes (from Google, open-source, scalable, microservices), Mesosphere DCOS (based on Apache Mesos but commerical), CoreOS fleet, OpenStack Magnum
