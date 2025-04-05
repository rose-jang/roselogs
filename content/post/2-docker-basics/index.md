---
title: Docker Basics
date: 2025-02-26
draft: false
image: docker-banner.png
tags:
  - Docker
  - Containerization
  - Virtualization
categories: 
  - Containerization
---

I journaled about the basics of Docker in this post. Starting with a brief overview of what docker is and concept of containerization. I delve into how containerization differs from traditional software deployment methods and conclude with a walkthrough of creating docker images and containers.

# What is Docker?

**`Docker`** is an open-source containerization platform (PaaS) that enables users to package applications along with their required dependencies into lightweight, portable containers. It simplifies application deployment and execution, making it a popular choice for modern software delivery.

---
## Why Docker?
### Benefits
- **Efficiency**
	Docker streamlines the deployment process with **pre-built images, reducing the complexity** of setting up environments from scratch. Containers save time and resources by eliminating the need for running a full operating system for each application.
- **Portability**
	Docker's Platform-agnostic containers provide consistent performance across various environments. Known for the resolution of "It works on my machine", **containers can run anywhere, not just on a local machine**.

### Virtualization VS Containerization
Virtualization is a technique that enables the execution of an entire operating system on a physical host using a **hypervisor**, such as `Hyper-V` or `VMware`. This allows multiple virtual machines to **run independently on its own resources** while being able to intercommunicate with each other.

Containerization on the other hand, focuses on packaging applications with their dependencies into containers that **share the resources of the host system**. Containers are more lightweight than VMs because they **don't require a full OS to run**. Instead, they run in isolated environments on the host operating system. 

# Core Concepts
## Behind-the-Scenes: How Docker Operates

Docker's powerful functionality stems from its core framework, **Docker Engine** that enables containerization. The combination of docker components allows Docker to pull base images from repositories, create containers, and manage them seamlessly. 

### Docker Engine Components
- **Docker Host**: Where the host system provides hardware resources to support operations.
- **Docker Daemon** (`dockerd`): Primary component that listens and processes user requests, and also responsible for managing images and containers.
- **Docker CLI**: The interface users interact for communicating with the Docker system conveniently. CLI interprets user commands into API requests for Docker Daemon.
- **REST API**: A stateless API enabling communication between the CLI and Docker Daemon to process and fulfill user requests.

### A little more about REST API...
- REST API is used for session communication between the user and the Docker Daemon. The Docker Daemon listens for REST API requests via `docker.sock` or over HTTP(S)/TCP protocols. Since REST APIs are stateless, they do not retain information about previous requests; each request is independent. This stateless nature works because the user includes all necessary information in each request to ensure it can be fulfilled without relying on prior context.

### Docker Engine Workflow
1. User initiates Docker (run via CLI or program).
2. Docker Daemon (dockerd) functions and listens for REST API requests via local socket or remote TCP socket.
3. User sends requests via CLI, which interprets the commands and forwards them as REST API requests to the Docker Daemon.
4. Docker Daemon processes the request and performs the desired action (e.g., creating a container, displays running containers).
5. User can then interact with Docker resources and experience the Docker system.

### Cross-Platform Operation
- **Docker Desktop**: Enables to run Linux based Docker system on Windows or macOS without additional emulation features. 
- **WSL Integration**: Integrating Docker Desktop with the `WSL (Windows Subsystem for Linux)` optimizes performances providing a native-like Linux environment for Windows users.

## Try Dockerfile

1. Start with **base images** available online such as `Docker Hub`
2. Create **custom images** by writing a `Dockerfile` script
3. The custom images are used to create & run containers
4. Containers operate in an isolated environment
	- Runs separately from the host system
	- Still relies on the host's resources (CPU, memory, storage, ...)

### Image
- **Image** is a static template used to create a container, which is editable and usable multiple times. 
- Edit `Dockerfike` if any updates needed for applications, very convenient & efficient way for development and deployment.

### Container - Port
When running a container, you get to configure port numbers. There are 2 port numbers which are used on host and container respectively. 
> `-p host-port:container-port` 
- `host-port` is opened externally for incoming traffics.
- `container-port` is at the door of containers listening to connections.
- Basically they map each other as you configured at container build.

### Create a Dockerfile
1. Specify and provide requirements in a `Dockerfile`
	- Define a desired base image 
	- Write required configurations, dependencies, or libraries
```dockerfile
FROM image:tag
RUN apt-get update && apt-get install -y nginx
COPY ./webServer
RUN ./web.sh
CMD ./conf.sh
```
2. Run the `Dockerfile` to create a container
	`docker -t image:tag directoryOfDockerfile`
	`docker -t webApp:first .`
	-> then Docker installs the listed dependencies or packages
3. Run the container
	`docker run -p 5000:443 --name myContainer webApp:first`

### Dockerfile - Best practice
1. Minimize image size
	- Use base images with the minimalist `alpine` Linux distribution
	- Install without cache using the flag `--no-cache-dir`
2. Keep the script clean
	- List a required dependencies in a file (.txt)
```dockerfile
FROM python:3.10-alpine
WORKDIR /kube-WebApp
COPY requirements.txt /kube-WebApp
RUN pip install -r dependencies.txt --no-cache-dir
COPY . /kube-WebApp
CMD python app.py
```

