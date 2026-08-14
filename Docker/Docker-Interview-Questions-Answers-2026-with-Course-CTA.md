# Docker Interview Questions & Answers --- 2026 Edition

Cracking your next DevOps/Cloud interview? These Docker interview
questions cover Docker fundamentals, images, Dockerfile, containers,
networking, storage, registries, security, optimization, Azure and
real-world troubleshooting scenarios.

Want to learn Docker with hands-on labs?

[Docker Masterclass -- Cloud Blogger
Academy](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)

------------------------------------------------------------------------

# 1. Docker Basics

## 1. What is Docker?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


Docker is an open-source containerization platform used to package,
distribute and run applications in isolated environments called
containers.

A Docker container contains:

-   Application code
-   Runtime
-   Libraries
-   Dependencies
-   Configuration required by the application

The main objective of Docker is to make applications run consistently
across different environments.

For example, suppose a developer develops a Python application on their
laptop.

The application requires:

``` text
Python 3.12
Flask
Requests
OpenSSL
Specific OS libraries
```

The developer's application works perfectly on their machine, but when
the application is deployed to another server, it may fail because of
different versions of Python or libraries.

Docker solves this problem by packaging the application and its
dependencies together.

The flow becomes:

``` text
Application Code
       |
       v
   Dockerfile
       |
       v
 docker build
       |
       v
 Docker Image
       |
       v
  docker run
       |
       v
Docker Container
```

### Important Docker Components

Docker mainly works with:

-   Docker Client
-   Docker Daemon
-   Docker Images
-   Docker Containers
-   Docker Networks
-   Docker Volumes
-   Docker Registry

### Example

Build an image:

``` bash
docker build -t myapp:v1 .
```

Run the container:

``` bash
docker run -d --name myapp myapp:v1
```

Check the container:

``` bash
docker ps
```

### Interview Answer

> Docker is a containerization platform that packages an application
> together with its dependencies and runtime into a portable container.
> It provides consistency across development, testing and production
> environments while using fewer resources than traditional virtual
> machines.

------------------------------------------------------------------------

## 2. Why do you use Docker containers instead of VMs?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


Docker containers and Virtual Machines solve different problems.

A Virtual Machine virtualizes hardware, while a container provides
operating-system-level isolation.

A VM contains:

``` text
Physical Server
      |
Hypervisor
      |
-------------------------
| VM 1 | VM 2 | VM 3 |
-------------------------
| OS   | OS   | OS   |
```

Every VM generally requires its own guest operating system.

Docker works differently:

``` text
Physical Server
      |
Host Operating System
      |
Docker Engine
      |
-------------------------
| Container | Container |
-------------------------
| App       | App       |
-------------------------
```

Containers share the host operating system kernel.

### Advantages of Containers

Containers are generally:

-   Lightweight
-   Faster to start
-   Easier to package
-   Easier to distribute
-   More efficient in resource usage
-   Suitable for microservices
-   Well suited for CI/CD

### VM vs Container

  Feature          Virtual Machine   Docker Container
  ---------------- ----------------- ----------------------
  Virtualization   Hardware          OS level
  Guest OS         Required          Usually not required
  Startup          Minutes/seconds   Usually seconds
  Size             Usually GBs       Often MBs/GBs
  Resource usage   Higher            Lower
  Isolation        Strong            Process-level
  Portability      Good              Very good

### When would you use a VM?

VMs are still useful when:

-   Full OS isolation is required.
-   You need a different operating system kernel.
-   Legacy applications require a complete OS.
-   Applications have special OS-level requirements.

### Interview Answer

> I use containers when I need lightweight, portable and fast
> application deployment. Containers reduce resource overhead because
> they share the host kernel, while VMs provide stronger OS-level
> isolation but require a complete guest operating system.

------------------------------------------------------------------------

## 3. How does a Docker container work?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


A Docker container is created from a Docker image.

For example:

``` bash
docker run nginx
```

Docker performs approximately the following process:

``` text
Docker Client
     |
     v
Docker Daemon
     |
     v
Check Local Image
     |
     +---- Image exists
     |
     +---- Image doesn't exist
              |
              v
         Docker Registry
              |
              v
         Pull Image
              |
              v
       Create Container
              |
              v
        Start Container
```

Docker uses Linux kernel features such as:

### Namespaces

Namespaces provide isolation.

For example, a container has its own:

-   Process namespace
-   Network namespace
-   Mount namespace
-   Hostname
-   IPC namespace

A process inside the container generally cannot see processes from
another isolated namespace.

### cgroups

Control groups, commonly called cgroups, are used to control and monitor
resource usage.

For example:

``` bash
docker run --memory=512m --cpus=1 nginx
```

This limits the container's resources.

### Container filesystem

Docker uses layered filesystems to create container filesystems.

An image consists of read-only layers, while the running container gets
a writable layer.

Conceptually:

``` text
Writable Container Layer
-------------------------
Image Layer
Image Layer
Base Image Layer
```

When the container is deleted, data stored only in the writable layer is
normally lost.

That is why Docker volumes are used for persistent data.

------------------------------------------------------------------------

## 4. Explain Docker architecture.

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


Docker uses a client-server architecture.

The main components are:

``` text
Docker Client
      |
      | Docker API
      v
Docker Daemon
      |
      +----------------+
      |                |
      v                v
   Images          Containers
      |
      v
 Docker Registry
```

### Docker Client

The Docker client is the command-line interface used by administrators
and developers.

Examples:

``` bash
docker ps
docker images
docker build
docker run
docker pull
docker push
```

### Docker Daemon

The Docker daemon manages Docker objects.

It is responsible for:

-   Creating containers
-   Starting containers
-   Stopping containers
-   Building images
-   Managing networks
-   Managing volumes

### Docker Images

Images are immutable templates used to create containers.

Example:

``` bash
docker pull nginx
```

### Docker Containers

Containers are running instances of Docker images.

``` bash
docker run -d nginx
```

### Docker Registry

A registry stores Docker images.

Examples include:

-   Docker Hub
-   Azure Container Registry
-   Amazon ECR
-   Google Artifact Registry
-   GitHub Container Registry

### Interview Answer

> Docker follows a client-server architecture where the Docker CLI
> communicates with the Docker daemon through an API. The daemon manages
> containers, images, networks and volumes, while registries are used to
> store and distribute images.

------------------------------------------------------------------------

## 5. What are Docker layers?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


Docker images are built using multiple filesystem layers.

Consider:

``` dockerfile
FROM ubuntu:24.04

RUN apt-get update

RUN apt-get install -y nginx

COPY index.html /var/www/html/
```

Conceptually, the image can be represented as:

``` text
Application Files
       |
Nginx Installation
       |
Package Metadata
       |
Ubuntu Base Image
```

Each Dockerfile instruction can create a new layer.

### Why are layers important?

Docker layers provide:

### Caching

If a layer hasn't changed, Docker can reuse it.

### Storage efficiency

Multiple images can share common layers.

For example:

``` text
Image A
  |
  +--- Ubuntu Layer
  +--- Python Layer
  +--- Application A

Image B
  |
  +--- Ubuntu Layer
  +--- Python Layer
  +--- Application B
```

The common layers can be shared.

### Faster builds

Docker can reuse unchanged layers.

### Docker history

You can inspect image layers using:

``` bash
docker history myapp:v1
```

------------------------------------------------------------------------

## 6. How is a Docker image created?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


The standard way to create a Docker image is through a Dockerfile.

Example:

``` dockerfile
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/

EXPOSE 80
```

Build the image:

``` bash
docker build -t my-nginx:v1 .
```

Explanation:

``` text
docker build
```

Tells Docker to build an image.

``` text
-t my-nginx:v1
```

Assigns the image name and tag.

``` text
.
```

Specifies the build context.

Check the image:

``` bash
docker images
```

Run it:

``` bash
docker run -d -p 8080:80 my-nginx:v1
```

Now the application can be accessed through the host's port 8080.

------------------------------------------------------------------------

## 7. Where do we keep Docker images?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


Docker images are stored in container registries.

Common registries include:

-   Docker Hub
-   Azure Container Registry
-   Amazon ECR
-   Google Artifact Registry
-   GitHub Container Registry

In an enterprise Azure environment, a typical architecture is:

``` text
Developer
   |
GitHub/GitLab
   |
CI/CD Pipeline
   |
Docker Build
   |
Security Scan
   |
Azure Container Registry
   |
AKS / Container Apps
```

------------------------------------------------------------------------

# Docker Images and Dockerfile

## 8. What is a Dockerfile?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


A Dockerfile is a text file containing instructions that Docker uses to
create an image.

Example:

``` dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["python", "app.py"]
```

The Dockerfile defines:

-   Base image
-   Working directory
-   Dependencies
-   Application files
-   Port
-   Startup command

Build it:

``` bash
docker build -t python-app:v1 .
```

Run it:

``` bash
docker run -d -p 5000:5000 python-app:v1
```

### Best Practice

Dockerfiles should be:

-   Small
-   Reproducible
-   Secure
-   Easy to maintain
-   Optimized for caching

------------------------------------------------------------------------

## 9. Explain the instructions used in a Dockerfile.

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


### FROM

Defines the base image.

``` dockerfile
FROM ubuntu:24.04
```

### WORKDIR

Sets the working directory.

``` dockerfile
WORKDIR /app
```

### COPY

Copies files from the build context into the image.

``` dockerfile
COPY . /app
```

### ADD

Similar to COPY but provides additional functionality.

Generally, `COPY` is preferred unless the additional ADD functionality
is specifically required.

### RUN

Executes a command during image creation.

``` dockerfile
RUN apt-get update
```

### ENV

Sets environment variables.

``` dockerfile
ENV APP_ENV=production
```

### ARG

Defines build-time variables.

``` dockerfile
ARG VERSION=1.0
```

### EXPOSE

Documents the port the application listens on.

``` dockerfile
EXPOSE 8080
```

Important: `EXPOSE` does not publish the port to the host.

For publishing, use:

``` bash
docker run -p 8080:8080 myapp
```

### CMD

Defines the default command.

``` dockerfile
CMD ["python", "app.py"]
```

### ENTRYPOINT

Defines the primary executable.

``` dockerfile
ENTRYPOINT ["python"]
```

### USER

Defines which user runs the application.

``` dockerfile
USER appuser
```

Using a non-root user is recommended for security.

------------------------------------------------------------------------

## 10. What is the difference between a base image and a golden image?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


A base image is the initial foundation used to create an application
image.

Example:

``` dockerfile
FROM ubuntu:24.04
```

A golden image is an organization-approved image that has been
standardized and hardened.

For example:

``` text
Enterprise Golden Image
       |
       +-- Approved OS
       +-- Security Patches
       +-- CIS Hardening
       +-- Monitoring Requirements
       +-- Security Configuration
       +-- Approved Packages
```

Developers can use the golden image as the starting point.

### Why use golden images?

They help organizations achieve:

-   Standardization
-   Security
-   Compliance
-   Faster development
-   Reduced configuration differences

### Interview Answer

> A base image is simply the foundation of an image, while a golden
> image is an organization-approved and hardened image that follows
> internal security, compliance and configuration standards.

------------------------------------------------------------------------

## 11. Explain how a multi-stage Dockerfile is created.

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


Multi-stage builds allow us to use multiple build stages inside one
Dockerfile.

Example:

``` dockerfile
FROM node:22 AS builder

WORKDIR /app

COPY package*.json .

RUN npm install

COPY . .

RUN npm run build


FROM nginx:alpine

COPY --from=builder /app/dist /usr/share/nginx/html
```

The first stage is used for building the application.

The second stage is used for running the application.

The final image does not need:

-   Node.js
-   npm
-   Build tools
-   Source compilation tools

It only contains the generated application and Nginx.

### Benefits

-   Smaller image
-   Reduced attack surface
-   Fewer vulnerabilities
-   Faster image transfer
-   Better production security

------------------------------------------------------------------------

## 12. What is the difference between CMD and ENTRYPOINT?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


Both define what happens when a container starts, but their behavior is
different.

### CMD

CMD provides a default command.

``` dockerfile
CMD ["nginx", "-g", "daemon off;"]
```

The command can be overridden.

### ENTRYPOINT

ENTRYPOINT defines the primary executable.

``` dockerfile
ENTRYPOINT ["python"]
```

Then:

``` bash
docker run myimage app.py
```

results conceptually in:

``` bash
python app.py
```

### Common Pattern

You can combine them:

``` dockerfile
ENTRYPOINT ["python"]
CMD ["app.py"]
```

Here:

``` text
ENTRYPOINT = executable
CMD = default argument
```

### Interview Answer

> I use ENTRYPOINT when the container should behave like a specific
> executable. I use CMD for default commands or arguments that users may
> want to override.

------------------------------------------------------------------------

## 13. What is the difference between docker build and docker commit?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


### docker build

Creates an image from a Dockerfile.

``` bash
docker build -t myapp:v1 .
```

This is the recommended approach because the build process is:

-   Repeatable
-   Version controlled
-   Automated
-   Auditable

### docker commit

Creates an image from the current state of a container.

``` bash
docker commit container1 myapp:v1
```

This can be useful for exploratory or debugging scenarios but is
generally not the preferred production image-building method.

### Production Approach

Use:

``` text
Dockerfile
   |
Git
   |
CI/CD
   |
docker build
   |
Image
```

instead of manually modifying containers and committing them.

------------------------------------------------------------------------

# Docker Container, Storage and Networking

## 14. What is a Docker volume?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


Docker volumes are persistent storage managed by Docker.

Normally, data stored in the container's writable layer disappears when
the container is removed.

Example:

``` text
Container
    |
Application Data
    |
Delete Container
    |
Data Lost
```

Using a volume:

``` text
Container
    |
    v
Docker Volume
    |
    v
Persistent Data
```

Create a volume:

``` bash
docker volume create appdata
```

Run a container:

``` bash
docker run -d \
  --name mysql \
  -v appdata:/var/lib/mysql \
  mysql
```

Even if the container is removed, the volume can remain.

List volumes:

``` bash
docker volume ls
```

Inspect:

``` bash
docker volume inspect appdata
```

------------------------------------------------------------------------

## 15. Explain Docker networking.

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


Docker networking allows containers to communicate with:

-   Other containers
-   Host systems
-   External applications
-   Internet services

Common network drivers include:

``` text
bridge
host
none
overlay
macvlan
```

For standalone Docker containers, the bridge network is commonly used.

Create a network:

``` bash
docker network create app-network
```

Run:

``` bash
docker run -d \
  --name web \
  --network app-network \
  nginx
```

Another container can communicate with `web` through the Docker network.

------------------------------------------------------------------------

## 16. What are the different types of Docker networks?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


### Bridge

Default network type for standalone containers.

``` bash
docker network create mynetwork
```

Containers attached to the same network can communicate.

### Host

The container uses the host's network namespace.

``` bash
docker run --network host nginx
```

This reduces network isolation.

### None

The container has no normal network connectivity.

``` bash
docker run --network none nginx
```

### Overlay

Used to connect containers across multiple Docker hosts, particularly
with Docker Swarm.

### Macvlan

Allows containers to appear as network devices on the physical network.

------------------------------------------------------------------------

## 17. How do containers communicate with each other?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


Containers should generally communicate using a user-defined Docker
network.

Example:

``` bash
docker network create backend
```

Start database:

``` bash
docker run -d \
  --name mysql \
  --network backend \
  mysql
```

Start application:

``` bash
docker run -d \
  --name app \
  --network backend \
  myapp
```

The application can connect to:

``` text
mysql:3306
```

Instead of using a container IP address.

Using service/container names is better because container IP addresses
can change.

------------------------------------------------------------------------

## 18. How do you persist data generated by a Docker container?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


There are several options.

### Docker Volume

``` bash
docker run \
  -v myvolume:/data \
  myapp
```

### Bind Mount

``` bash
docker run \
  -v /host/data:/container/data \
  myapp
```

### External Storage

For cloud deployments, applications may use:

-   Azure Files
-   Azure Managed Disks
-   Azure Blob Storage
-   Amazon EFS
-   Amazon S3
-   Managed databases

For production, the storage architecture should depend on the
application's data requirements.

------------------------------------------------------------------------

# Docker Registry

## 19. What is Docker Hub?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


Docker Hub is a container registry provided by Docker.

It can be used to:

-   Store images
-   Pull images
-   Push images
-   Share images
-   Manage repositories

Pull an image:

``` bash
docker pull nginx
```

Tag an image:

``` bash
docker tag myapp:v1 username/myapp:v1
```

Push:

``` bash
docker push username/myapp:v1
```

Docker Hub contains many public images, but organizations should verify
and scan public images before using them in production.

------------------------------------------------------------------------

## 20. What is Azure Container Registry?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


Azure Container Registry, or ACR, is Microsoft's managed private
container registry.

It is designed for storing and managing container images and OCI
artifacts.

Typical architecture:

``` text
Developer
    |
GitHub/GitLab
    |
CI/CD
    |
Docker Build
    |
Security Scan
    |
ACR
    |
AKS
```

ACR supports integration with Azure identity and access control.

------------------------------------------------------------------------

## 21. What is the difference between ACR and Docker Hub?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


  Feature                      Docker Hub   ACR
  ---------------------------- ------------ ------------------
  Provider                     Docker       Microsoft
  Primary ecosystem            Docker       Azure
  Private repositories         Yes          Yes
  Azure integration            Limited      Native
  Azure RBAC                   No           Yes
  Entra integration            No           Yes
  Enterprise Azure workloads   Possible     Excellent choice

If an organization is already heavily invested in Azure, ACR is
generally a natural choice for private container images.

------------------------------------------------------------------------

## 22. Why would you use ACR instead of Docker Hub?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


I would choose ACR in an Azure enterprise environment because of:

-   Azure RBAC
-   Microsoft Entra integration
-   Private repositories
-   Integration with AKS
-   Integration with Azure Container Apps
-   Azure security ecosystem
-   Enterprise governance
-   Geo-replication capabilities
-   Network access controls

The architecture becomes:

``` text
GitLab
  |
CI/CD
  |
ACR
  |
AKS
```

This reduces the need to use a public registry for production images.

------------------------------------------------------------------------

## 23. Where would you store Docker images in an enterprise environment?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


It depends on the cloud environment.

For Azure:

``` text
Azure Container Registry
```

For AWS:

``` text
Amazon ECR
```

For Google Cloud:

``` text
Artifact Registry
```

For multi-cloud environments, organizations may use multiple registries
or a centralized registry strategy.

The important requirements are:

-   Authentication
-   Authorization
-   Vulnerability scanning
-   Image lifecycle management
-   Image immutability/tagging strategy
-   Network security
-   Audit logging

------------------------------------------------------------------------

## 24. How do you push and pull an image from ACR?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


Login to Azure:

``` bash
az login
```

Login to ACR:

``` bash
az acr login --name myregistry
```

Build:

``` bash
docker build -t myapp:v1 .
```

Tag:

``` bash
docker tag myapp:v1 myregistry.azurecr.io/myapp:v1
```

Push:

``` bash
docker push myregistry.azurecr.io/myapp:v1
```

Pull:

``` bash
docker pull myregistry.azurecr.io/myapp:v1
```

List repositories:

``` bash
az acr repository list \
  --name myregistry \
  --output table
```

------------------------------------------------------------------------

# Application to Docker Deployment

## 25. If a developer gives you application code, how will you deploy it using Docker?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


I would follow a structured process.

``` text
Application Code
       |
Understand Application
       |
Identify Dependencies
       |
Create Dockerfile
       |
Create .dockerignore
       |
Build Image
       |
Run Container
       |
Test Application
       |
Security Scan
       |
Push Image to Registry
       |
Deploy to Environment
```

I would first understand:

-   Programming language
-   Framework
-   Dependencies
-   Build command
-   Startup command
-   Application port
-   Environment variables
-   External services

Then I would create the Dockerfile.

------------------------------------------------------------------------

## 26. What steps do you follow to create a Docker image from application code?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


My process would be:

1.  Identify application runtime.
2.  Select appropriate base image.
3.  Create Dockerfile.
4.  Create `.dockerignore`.
5.  Install dependencies.
6.  Copy application source.
7.  Define required port.
8.  Define startup command.
9.  Build the image.
10. Test the image.
11. Scan the image.
12. Push it to the registry.

Example:

``` bash
docker build -t myapp:v1 .
```

------------------------------------------------------------------------

## 27. How do you run the Docker container?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


Basic:

``` bash
docker run nginx
```

Detached mode:

``` bash
docker run -d nginx
```

Named container:

``` bash
docker run -d --name web nginx
```

Port mapping:

``` bash
docker run -d \
  --name web \
  -p 8080:80 \
  nginx
```

Environment variable:

``` bash
docker run -d \
  -e APP_ENV=production \
  myapp
```

Volume:

``` bash
docker run -d \
  -v appdata:/data \
  myapp
```

Network:

``` bash
docker run -d \
  --network backend \
  myapp
```

------------------------------------------------------------------------

## 28. How do you expose the application running inside a container?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


There are two concepts.

### EXPOSE

Dockerfile:

``` dockerfile
EXPOSE 8080
```

This documents the port.

It does not automatically publish the port.

### Port Publishing

Use:

``` bash
docker run -p 8080:8080 myapp
```

The format is:

``` text
Host Port : Container Port
```

For example:

``` text
8080:80
```

means:

``` text
Host Port = 8080
Container Port = 80
```

------------------------------------------------------------------------

## 29. How do you pass environment variables and configuration to a container?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


Using:

``` bash
docker run \
  -e APP_ENV=production \
  -e DB_HOST=mysql \
  myapp
```

Multiple variables can be passed.

Alternatively:

``` bash
docker run \
  --env-file .env \
  myapp
```

For production environments, secrets should not be hardcoded in
Dockerfiles.

Instead, use appropriate secret-management solutions such as:

-   Azure Key Vault
-   Kubernetes Secrets
-   CI/CD secret variables
-   Managed identity
-   Cloud-native secret stores

------------------------------------------------------------------------

## 30. What was your primary method of deployment --- Virtual Machines or Container Services? Why?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


A strong interview answer depends on the actual project experience.

For a modern application:

> For traditional or legacy workloads, I have used Virtual Machines
> where full operating-system control was required. For modern
> applications and microservices, I prefer containers because they
> provide consistent packaging, faster deployment and easier
> scalability. In Azure, depending on the workload, I would use Azure
> Container Apps for simpler serverless container deployments and AKS
> when Kubernetes-level control and orchestration are required.

The choice depends on:

-   Application architecture
-   Scalability
-   Operational requirements
-   Team expertise
-   Security
-   Cost
-   Availability requirements

------------------------------------------------------------------------

# Docker Security

## 31. How do you secure Docker?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


Docker security should be implemented at multiple levels.

### Image Security

Use trusted base images.

Scan images:

``` bash
trivy image myapp:v1
```

### Container Security

Run as non-root:

``` dockerfile
USER appuser
```

### Secret Security

Never put passwords directly inside Dockerfiles.

### Resource Security

Use CPU and memory limits:

``` bash
docker run \
  --memory=512m \
  --cpus=1 \
  myapp
```

### Network Security

Only expose required ports.

### Registry Security

Use private registries and proper access control.

### Supply Chain Security

Use:

-   Approved base images
-   Vulnerability scanning
-   Image signing
-   Provenance
-   CI/CD policies

------------------------------------------------------------------------

## 32. How do you scan a Docker image?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


Several tools are available.

Examples:

-   Trivy
-   Docker Scout
-   Snyk
-   Microsoft Defender for Cloud
-   Clair

Example:

``` bash
trivy image myapp:v1
```

A scanner can identify vulnerabilities in:

-   Operating system packages
-   Application dependencies
-   Libraries
-   Configuration

A CI/CD pipeline can fail the build when vulnerabilities exceed an
approved severity threshold.

------------------------------------------------------------------------

## 33. Which tools can be used for Docker image vulnerability scanning?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


Common tools include:

### Trivy

Popular open-source vulnerability scanner.

### Docker Scout

Docker's tooling for image analysis and software supply-chain insights.

### Snyk

Provides vulnerability scanning for containers and dependencies.

### Microsoft Defender for Cloud

Useful in Azure environments for cloud security and container security.

### Clair

Open-source container vulnerability scanner.

In an enterprise environment, the choice depends on the organization's
security platform and CI/CD architecture.

------------------------------------------------------------------------

## 34. How do you handle vulnerabilities found in a Docker image?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


I would not simply ignore the vulnerability.

The process should be:

``` text
CVE Detected
     |
Check Severity
     |
Identify Package
     |
Check Exploitability
     |
Find Patched Version
     |
Update Dependency/Base Image
     |
Rebuild
     |
Rescan
     |
Test
     |
Deploy
```

For example, if the base image contains an outdated OpenSSL package, I
would first check whether a patched base image is available.

Then:

``` bash
docker build -t myapp:v2 .
```

Scan again:

``` bash
trivy image myapp:v2
```

Only after validation should the new image move toward production.

------------------------------------------------------------------------

## 35. A critical vulnerability is found in a production image. What steps will you take?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


I would first determine:

-   CVE severity
-   Whether it is exploitable
-   Whether the vulnerable component is actually used
-   Whether the container is internet-facing
-   Whether a patched version exists
-   Whether active exploitation is occurring

Then I would:

1.  Notify the relevant security/application teams.
2.  Identify the affected image versions.
3.  Build a patched image.
4.  Run vulnerability scans.
5.  Perform application testing.
6.  Deploy using the standard deployment process.
7.  Monitor the new version.

If the risk is severe and actively exploitable, I would follow the
organization's incident-response procedure and consider isolation or
emergency mitigation rather than blindly stopping production.

------------------------------------------------------------------------

## 36. How do you ensure that only trusted images are deployed in production?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


I would establish an image supply-chain process.

``` text
Source Code
    |
CI/CD
    |
Approved Base Image
    |
Build
    |
Security Scan
    |
Image Signing
    |
Private Registry
    |
Policy Validation
    |
Production
```

Controls can include:

-   Approved registries
-   Approved base images
-   Vulnerability scanning
-   Image signing
-   Immutable tags/digests
-   RBAC
-   Admission policies
-   Audit logs

For production, I would prefer image digests over relying only on
mutable tags such as `latest`.

------------------------------------------------------------------------

## 37. Why should containers run as a non-root user?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


By default, some containers may run processes as root.

If the application is compromised, root privileges could increase the
impact.

Example:

``` dockerfile
FROM python:3.12-slim

RUN useradd -m appuser

WORKDIR /app

COPY . .

USER appuser

CMD ["python", "app.py"]
```

Now the application runs as `appuser` instead of root.

This follows the principle of least privilege.

Other security practices include:

-   Read-only filesystem
-   Dropping unnecessary Linux capabilities
-   No privileged containers unless required
-   Resource limits
-   Network restrictions

------------------------------------------------------------------------

# Docker Performance and Optimization

## 38. If a Docker image is taking too long to build, how would you optimize it?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


I would investigate Docker build performance systematically.

First:

``` bash
docker build --progress=plain -t myapp:v1 .
```

Then I would check:

### Build context

Large build contexts slow down builds.

Use:

``` text
.dockerignore
```

### Layer caching

Structure Dockerfile so stable dependencies are installed before
frequently changing application code.

Bad:

``` dockerfile
COPY . .
RUN npm install
```

Better:

``` dockerfile
COPY package*.json .
RUN npm install

COPY . .
```

If source code changes but package files don't, Docker can reuse the
dependency installation layer.

### Multi-stage builds

Use multi-stage builds to separate compilation from runtime.

### BuildKit

Use modern Docker build functionality for improved build performance and
caching.

------------------------------------------------------------------------

## 39. If a Docker image is taking too long to pull in the pipeline, how would you optimize it?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


I would first check the image size.

``` bash
docker images
```

Then inspect layers:

``` bash
docker history myapp:v1
```

Optimization steps:

1.  Reduce base image size.
2.  Remove unnecessary packages.
3.  Use multi-stage builds.
4.  Remove build dependencies.
5.  Use `.dockerignore`.
6.  Reduce unnecessary layers.
7.  Keep the registry close to the workload.
8.  Use caching where supported.
9.  Use immutable image versions.

For Azure workloads, using ACR appropriately can improve image
distribution.

------------------------------------------------------------------------

## 40. How can you reduce Docker image size?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


The main techniques are:

### Use smaller base images

Use a suitable slim or minimal image where compatible.

### Multi-stage builds

Build the application in one stage and run it in another.

### Remove unnecessary packages

Do not install packages that are not required at runtime.

### Use `.dockerignore`

Example:

``` text
.git
node_modules
*.log
.env
tests
README.md
```

### Clean package caches

Package-manager cache files should not unnecessarily remain in the final
image.

### Inspect layers

``` bash
docker history myapp:v1
```

------------------------------------------------------------------------

## 41. How do Docker layer caching and .dockerignore help improve build performance?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


Docker layer caching means Docker can reuse previously created layers
when the relevant Dockerfile instructions and inputs have not changed.

Example:

``` dockerfile
COPY package*.json .

RUN npm install

COPY . .
```

If only `app.js` changes, Docker can reuse the `npm install` layer
instead of running it again.

`.dockerignore` reduces the build context.

Example:

``` text
.git
node_modules
*.log
.env
```

This provides:

-   Smaller build context
-   Faster transfer
-   Faster builds
-   Reduced accidental inclusion of sensitive files

------------------------------------------------------------------------

## 42. Why would you use a multi-stage Docker build for optimization?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


A multi-stage build allows us to keep build-time dependencies out of the
final production image.

For example:

``` text
Build Stage
------------------
Compiler
npm
Build Tools
Source Code
Dependencies
------------------

        |
        v

Production Stage
------------------
Runtime
Application
Required Libraries
------------------
```

The final image becomes smaller and contains fewer packages.

This improves:

-   Pull time
-   Startup efficiency
-   Security
-   Vulnerability management
-   Deployment speed

------------------------------------------------------------------------

# Azure Container Services

## 43. What is ACR and how does it integrate with Azure services?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


Azure Container Registry is a managed container registry.

A common architecture is:

``` text
GitHub / GitLab
       |
       v
CI/CD Pipeline
       |
       v
Docker Build
       |
       v
Security Scan
       |
       v
ACR
       |
       +----------+
       |          |
       v          v
      AKS     Container Apps
```

ACR can integrate with Azure identity and access-control mechanisms.

For AKS, the cluster can be granted appropriate permissions to pull
images from ACR.

------------------------------------------------------------------------

## 44. How would you deploy a Docker container on Azure?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


There are several options.

### Azure Container Apps

Suitable for serverless containerized applications.

### Azure Kubernetes Service

Suitable when Kubernetes orchestration is required.

### Azure Container Instances

Useful for simple container execution without managing a Kubernetes
cluster.

### Azure Virtual Machines

Useful when full operating-system control is required.

The selection depends on:

-   Application architecture
-   Scaling requirements
-   Kubernetes requirements
-   Operational complexity
-   Cost
-   Networking
-   Security requirements

------------------------------------------------------------------------

## 45. Which Azure service can be used for serverless container deployment?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


Azure Container Apps is an Azure service designed to run containerized
applications without requiring the customer to manage Kubernetes
infrastructure directly.

It provides features such as:

-   Ingress
-   Autoscaling
-   Revisions
-   Secrets
-   Managed identity
-   Microservice-oriented deployment patterns

Example architecture:

``` text
Developer
    |
Docker Image
    |
ACR
    |
Azure Container Apps
    |
Application
```

------------------------------------------------------------------------

## 46. What is the difference between Azure Container Apps and AKS?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


  -------------------------------------------------------------------------
  Area                    Azure Container Apps      AKS
  ----------------------- ------------------------- -----------------------
  Platform                Serverless container      Managed Kubernetes
                          platform                  

  Complexity              Lower                     Higher

  Kubernetes management   Abstracted                Direct Kubernetes
                                                    experience

  Cluster management      Minimal                   Required

  Kubernetes API control  Limited compared with AKS Full

  Advanced networking     More abstracted           Highly configurable

  Custom Kubernetes       Limited                   Supported
  operators                                         

  Best suited for         APIs/microservices/jobs   Complex Kubernetes
                                                    workloads
  -------------------------------------------------------------------------

### Interview Answer

> I would choose Azure Container Apps when I want to deploy containers
> with minimal infrastructure management. I would choose AKS when I need
> Kubernetes-native functionality, advanced networking, custom
> controllers, complex scheduling or greater cluster-level control.

------------------------------------------------------------------------

## 47. How would you deploy a Docker image from ACR to AKS?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


First, build the image:

``` bash
docker build -t myapp:v1 .
```

Tag it:

``` bash
docker tag myapp:v1 myregistry.azurecr.io/myapp:v1
```

Push:

``` bash
docker push myregistry.azurecr.io/myapp:v1
```

Then create a Kubernetes Deployment:

``` yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
        - name: myapp
          image: myregistry.azurecr.io/myapp:v1
          ports:
            - containerPort: 8080
```

Apply:

``` bash
kubectl apply -f deployment.yaml
```

Check:

``` bash
kubectl get pods
```

The AKS cluster needs appropriate authorization to pull the image from
ACR.

------------------------------------------------------------------------

## 48. Why would you choose AKS instead of Azure Container Apps?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


I would choose AKS when the workload requires advanced Kubernetes
capabilities.

Examples:

-   Kubernetes-native application
-   Custom operators
-   Advanced scheduling
-   Stateful workloads
-   Complex networking
-   Service mesh
-   Custom controllers
-   Kubernetes ecosystem integrations
-   Fine-grained cluster control

Container Apps would generally be preferred when the goal is to run
containers without taking on as much Kubernetes operational complexity.

------------------------------------------------------------------------

# Scenario-Based Docker Questions

## 49. A developer gives you code but no Dockerfile. What will you do?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


I would not immediately create a random Dockerfile.

First, I would understand the application.

I would identify:

``` text
Programming Language
Framework
Dependency Files
Build Process
Startup Command
Application Port
Environment Variables
External Dependencies
```

For example, if it is a Node.js application:

``` text
package.json
package-lock.json
```

would tell me about dependencies.

Then I would create:

``` text
Dockerfile
.dockerignore
```

Build:

``` bash
docker build -t myapp:v1 .
```

Run:

``` bash
docker run -d -p 8080:8080 myapp:v1
```

Test the application.

Then scan:

``` bash
trivy image myapp:v1
```

Finally push it to ACR.

------------------------------------------------------------------------

## 50. Your Docker build is failing in the CI/CD pipeline. How will you troubleshoot it?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


I would follow a systematic troubleshooting process.

First identify the exact failing stage.

For local debugging:

``` bash
docker build --progress=plain -t myapp:test .
```

Then check:

### Dockerfile

-   Syntax
-   Incorrect instructions
-   Wrong paths

### Base image

Verify that the image exists and can be pulled.

### Registry

Check authentication and permissions.

### Build context

Check `.dockerignore`.

### Dependencies

Check whether package repositories are accessible.

### Runner

Check:

-   CPU
-   Memory
-   Disk
-   Docker daemon
-   Network

### Authentication

Verify CI/CD credentials.

I would avoid changing multiple things at once because that makes
troubleshooting difficult.

------------------------------------------------------------------------

## 51. The Docker image is 2 GB and takes a long time to pull. How will you reduce deployment time?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


First:

``` bash
docker history myapp:v1
```

I would identify which layers are consuming the most space.

Then:

1.  Select a smaller suitable base image.
2.  Use multi-stage builds.
3.  Remove build dependencies.
4.  Remove unnecessary packages.
5.  Add `.dockerignore`.
6.  Remove unnecessary files.
7.  Clean package caches.
8.  Optimize Dockerfile layers.
9.  Use appropriate registry placement.
10. Use immutable versioned images.

For example:

``` text
2 GB Image
   |
Analyze Layers
   |
Remove Build Tools
   |
Multi-stage Build
   |
Minimal Runtime Image
   |
500 MB Image
```

The actual reduction depends on the application.

------------------------------------------------------------------------

## 52. A container starts and immediately stops. How will you troubleshoot it?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


First:

``` bash
docker ps -a
```

This shows stopped containers.

Then:

``` bash
docker logs <container>
```

This is usually the first place to look for application errors.

Then:

``` bash
docker inspect <container>
```

I would check:

-   Exit code
-   Command
-   Environment variables
-   Mounts
-   Network
-   Configuration

A container normally remains running only while its primary process
remains running.

For example:

``` dockerfile
CMD ["python", "app.py"]
```

If `app.py` exits, the container exits.

------------------------------------------------------------------------

## 53. The application works locally but fails inside Docker. What will you check?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


I would check the environment difference.

### Configuration

Are the required environment variables available?

### Networking

Can the container reach:

-   Database
-   API
-   External service

### Ports

Is the application listening on the expected port?

### Binding

Is it listening on:

``` text
0.0.0.0
```

rather than only:

``` text
127.0.0.1
```

### File paths

Linux paths and local paths may differ.

### Permissions

Does the application user have access to required files?

### Dependencies

Are all runtime dependencies installed?

### OS libraries

Some applications depend on system libraries that may not exist in the
container.

------------------------------------------------------------------------

## 54. Your production container has a critical CVE. Will you immediately stop the container?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


Not necessarily.

Stopping a production application immediately could cause an outage.

I would first assess:

-   CVE severity
-   Exploitability
-   Exposure
-   Whether the affected component is used
-   Whether compensating controls exist
-   Whether a patched image is available

If the vulnerability is actively exploitable and the business risk is
critical, emergency mitigation may be required.

Otherwise, I would:

``` text
Identify CVE
    |
Build Patched Image
    |
Scan
    |
Test
    |
Deploy
    |
Monitor
```

The decision should follow the organization's security and
incident-response process.

------------------------------------------------------------------------

## 55. The container cannot connect to another container. How will you troubleshoot it?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


First check networks:

``` bash
docker network ls
```

Inspect:

``` bash
docker network inspect <network>
```

Check containers:

``` bash
docker ps
```

Verify that both containers are attached to the same network.

For example:

``` text
app
 |
 | backend network
 |
mysql
```

Then verify:

-   Container/service name
-   Port
-   DNS resolution
-   Application listening address
-   Firewall rules
-   Network configuration

From the application container, I may also test connectivity using
suitable diagnostic tools available in the image.

------------------------------------------------------------------------

## 56. A container is consuming very high CPU/memory. How will you investigate?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


First:

``` bash
docker stats
```

This gives real-time resource usage.

Example:

``` text
CONTAINER    CPU %    MEM USAGE
app          95%      1.8GB
mysql        10%      500MB
```

Then I would investigate:

### Application logs

``` bash
docker logs app
```

### Processes

``` bash
docker top app
```

### Container configuration

``` bash
docker inspect app
```

I would also check whether resource limits are configured.

Example:

``` bash
docker run \
  --cpus=1 \
  --memory=512m \
  myapp
```

For production Kubernetes workloads, I would additionally use Kubernetes
metrics and monitoring tools.

------------------------------------------------------------------------

## 57. Developers want to use a public Docker image in production. What checks will you perform?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


I would not directly deploy the public image.

I would check:

### Publisher

Who created the image?

### Source

Is the source code publicly available?

### Maintenance

When was the image last updated?

### Vulnerabilities

Scan the image:

``` bash
trivy image image-name:tag
```

### Dependencies

Check OS and application packages.

### License

Verify licensing requirements.

### Security

Check for:

-   Root user
-   Unnecessary packages
-   Exposed ports
-   Suspicious binaries
-   Embedded secrets

### Enterprise policy

If approved, I would ideally mirror or rebuild the image using the
organization's approved base image and store the resulting image in the
private registry.

------------------------------------------------------------------------

## 58. How would you design a secure Docker-based deployment for a production application?

> **Learn Docker with Hands-on Labs — ₹999**  
> Master Docker through practical labs, real-world scenarios, Dockerfile, containers, networking, storage, Docker Hub, ACR, security and Azure deployment.  
> [Enroll in the Docker Course for ₹999](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)


I would design the complete container lifecycle rather than only
focusing on the Docker container.

Architecture:

``` text
                 Developer
                     |
                     v
              Git Repository
                     |
                     v
              CI/CD Pipeline
                     |
                     v
              Docker Build
                     |
                     v
            Vulnerability Scan
                     |
                     v
          Image Validation/Signing
                     |
                     v
            Private ACR Registry
                     |
                     v
          AKS / Azure Container Apps
                     |
          +----------+----------+
          |                     |
          v                     v
     Monitoring              Logging
          |                     |
          +----------+----------+
                     |
                     v
                Alerting
```

## Security Controls

### 1. Use trusted base images

Do not randomly select public images.

### 2. Use minimal images

Reduce unnecessary packages.

### 3. Use multi-stage builds

Keep build dependencies out of production.

### 4. Run as non-root

``` dockerfile
USER appuser
```

### 5. Scan images

Use tools such as Trivy, Docker Scout or enterprise security platforms.

### 6. Protect secrets

Do not put passwords inside:

``` dockerfile
ENV
```

or:

``` text
Dockerfile
```

Use appropriate secret management.

### 7. Use private registry

Store production images in ACR.

### 8. Implement RBAC

Only authorized users and workloads should be able to push or deploy
images.

### 9. Use image versions/digests

Avoid relying only on:

``` text
latest
```

### 10. Apply resource limits

Prevent a container from consuming unlimited resources.

### 11. Network segmentation

Only allow required communication.

### 12. Monitoring

Monitor:

-   CPU
-   Memory
-   Network
-   Application health
-   Container restarts
-   Security events

### 13. CI/CD Governance

The pipeline should enforce:

``` text
Build
  ↓
Test
  ↓
Scan
  ↓
Validate
  ↓
Push
  ↓
Deploy
  ↓
Monitor
```

### Interview Answer

> In a production Docker environment, I would implement security across
> the complete container lifecycle. I would use trusted and minimal base
> images, multi-stage builds, non-root containers, vulnerability
> scanning, private ACR, RBAC, secure secret management, image
> validation, resource limits, network controls and monitoring. The goal
> is to secure not only the container but the complete software supply
> chain from source code to production deployment.

------------------------------------------------------------------------

# Recommended GitHub Structure

``` text
Docker-Interview-Questions/
│
├── README.md
├── 01-Docker-Basics.md
├── 02-Docker-Images-Dockerfile.md
├── 03-Containers-Networking-Storage.md
├── 04-Docker-Registry.md
├── 05-Docker-Deployment.md
├── 06-Docker-Security.md
├── 07-Docker-Optimization.md
├── 08-Azure-Container-Services.md
└── 09-Docker-Scenario-Based-Questions.md
```

## Hands-on Docker Masterclass

Learn Docker through practical labs covering:

-   Docker installation
-   Docker images
-   Docker containers
-   Dockerfile
-   Docker networking
-   Docker volumes
-   Docker Hub
-   Azure Container Registry
-   Docker security
-   Docker optimization
-   Docker CI/CD
-   Azure container deployment

[Cloud Blogger Academy --- Docker
Course](https://www.cloudbloggeracademy.com/courses/Docker-6a6a04d02ca536c954b431c7)
