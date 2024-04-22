# What is Docker
* Docker is an open source platform that enables developers to build, deploy, run, update and manage containers—standardized, executable components that combine application source code with the operating system (OS) libraries and dependencies required to run that code in any environment.

<img src="https://github.com/pentest-khoa-02/TheMinh/blob/main/Week%204/images/4.png" width="666px" align="center">

# Why use Docker?
* Docker is so popular today that “Docker” and “containers” are used interchangeably. But the first container-related technologies were available for years—even decades (link resides outside ibm.com)—before Docker was released to the public in 2013. 

* Docker lets developers access these native containerization capabilities using simple commands and automate them through a work-saving application programming interface (API). Compared to LXC, Docker offers:
    - Improved and seamless container portability: While LXC containers often reference machine-specific configurations, Docker containers run without modification across any desktop, data center and cloud environment. 

    - Even lighter weight and more granular updates: With LXC, multiple processes can be combined within a single container. This flexibility makes it possible to build an application that can continue running while one of its parts is taken down for an update or repair. 

    - Automated container creation: Docker can automatically build a container based on application source code. 

    - Container versioning: Docker can track versions of a container image, roll back to previous versions and trace who built a version and how. It can even upload only the deltas between an existing version and a new one. 

    - Container reuse: Existing containers can be used as base images—essentially like templates for building new containers. 

    - Shared container libraries: Developers can access an open source registry containing thousands of user-contributed containers. 
# Docker tools and terms
## Docker Hub
* Docker Hub (link resides outside ibm.com) is the public repository of Docker images that calls itself the “world’s largest library and community for container images.” It holds over 100,000 container images sourced from commercial software vendors, open source projects and individual developers. It includes images that have been produced by Docker, Inc., certified images belonging to the Docker Trusted Registry and thousands of other images. 

* All Docker Hub users can share their images at will. They can also download predefined base images from the Docker filesystem to use as a starting point for any containerization project. 

<img src="https://github.com/pentest-khoa-02/TheMinh/blob/main/Week%204/images/3.png" width="666px" align="center">

* Other image repositories exist, as well, notably GitHub. GitHub is a repository hosting service, well known for application development tools and as a platform that fosters collaboration and communication. Users of Docker Hub can create a repository (repo) which can hold many images. The repository can be public or private and can be linked to GitHub or BitBucket accounts. 

## Docker images

* Docker images contain executable application source code as well as all the tools, libraries and dependencies that the application code needs to run as a container. When you run the Docker image, it becomes one instance (or multiple instances) of the container. 

* It’s possible to build a Docker image from scratch, but most developers pull them down from common repositories. Multiple Docker images can be created from a single base image and they’ll share the commonalities of their stack. 

* Docker images are made up of layers and each layer corresponds to a version of the image. Whenever a developer makes changes to the image, a new top layer is created and this top layer replaces the previous top layer as the current version of the image. Previous layers are saved for rollbacks or to be re-used in other projects. 

* Each time a container is created from a Docker image, yet another new layer called the container layer is created. Changes made to the container—such as the addition or deletion of files—are saved to the container layer and exist only while the container is running.

* This iterative image-creation process enables increased overall efficiency since multiple live container instances can run from just a single base image and when they do so, they leverage a common stack. 

## Dockerfile
* Every Docker container starts with a simple text file containing instructions for how to build the Docker container image. Dockerfile automates the process of Docker image creation. It’s essentially a list of command-line interface (CLI) instructions that Docker Engine will run in order to assemble the image. The list of Docker commands is huge, but standardized: Docker operations work the same regardless of contents, infrastructure or other environment variables. 

<img src="https://github.com/pentest-khoa-02/TheMinh/blob/main/Week%204/images/1.png" width="666px" align="center">

## Docker containers
* Docker containers are the live, running instances of Docker images. While Docker images are read-only files, containers are live, ephemeral, executable content. Users can interact with them and administrators can adjust their settings and conditions using Docker commands. 

<img src="https://github.com/pentest-khoa-02/TheMinh/blob/main/Week%204/images/2.png" width="666px" align="center">

## Docker Desktop
* Docker Desktop (link resides outside ibm.com) is an application for Mac or Windows that includes Docker Engine, Docker CLI client, Docker Compose, Kubernetes and others. It also includes access to Docker Hub. 

## Docker daemon
* Docker daemon is a service that creates and manages Docker images, using the commands from the client. Essentially the Docker daemon serves as the control center of your Docker implementation. The server on which Docker daemon runs is called the Docker host.

## Docker registry
* A Docker registry is a scalable open source storage and distribution system for Docker images. The registry enables you to track image versions in repositories, using tagging for identification. This tracking and identification is accomplished using Git, a version control tool. 
