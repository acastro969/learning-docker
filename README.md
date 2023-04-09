# Docker

Docker is a container platform that allows you to package applications along with their dependencies and configurations, and run them in isolation in any environment. A Docker container is an instance of a running Docker image. In other words, it is a kind of virtualized and isolated environment where the application runs, built from a Docker image. Each Docker container is independent and does not interact with other containers unless specifically configured to do so.

Containers are portable and easy to share, simplifying the deployment and development of applications. Docker containers can be stored in a container registry, such as Docker Hub, which is a public repository where popular application images, such as Node.js, Python, Golang, MySQL, among others, can be found.

## Configuration and Dependency Issues

Before containers, it was common to have problems with application configuration and dependencies, especially in heterogeneous environments with different operating systems and software versions. Installation processes could be very different from each other, increasing the risk of errors and deployment failures.
Automation with Docker

With Docker, the application installation and configuration process can be automated, and all dependencies can be made available in any environment.

## Development with Docker

In development with Docker, an image containing the necessary dependencies and configuration files is downloaded from a container registry. With just one command, the application can be up and running on the development machine.

## Deployment with Docker

In deployment with Docker, an application image is built and published to a container registry. The image can then be run in any environment that has Docker installed, ensuring that the application runs consistently without configuration or dependency issues.

In summary, Docker simplifies the development and deployment of applications by packaging them with their dependencies and configurations into containers that are portable and easy to share. This reduces errors and downtime in deployment, increasing the efficiency and productivity of the development team.

## Virtualization

The concept of virtualization refers to the ability to run multiple operating systems or applications on a single physical machine. Virtualization is based on three main layers: hardware, kernel, and applications. In the case of virtual machines, both the kernel and the applications are virtualized, which can make images very large due to the inclusion of multiple operating systems.

However, Docker uses a container architecture that only virtualizes the application layer. Additionally, instead of including a complete kernel, Docker uses the host operating system kernel, meaning it runs directly on the physical hardware of the computer. This makes Docker containers much lighter compared to virtual machines, with sizes of just a few hundred megabytes.

## Images or Containers?

In Docker, an image is a self-contained package that includes an application's code, its dependencies, and the instructions to run it. On the other hand, a container is a running instance of an image. In other words, an image is like a blueprint or a recipe, while a container is the application itself, ready to be executed. When a container is run, an isolated environment is created in which the application runs, with its own file system, network, and resources, allowing multiple containers to coexist on the same physical machine without interfering with each other.

## Docker Desktop

Docker Desktop allows users to run containers and manage their images. It is a software platform that runs natively on Windows, macOS, and Linux operating systems. Docker Desktop provides an easy-to-use graphical user interface (GUI) for users to interact with containers and images. It also includes tools such as Docker Compose and CLI (Command Line Interface).

On Windows, Docker Desktop runs natively using WSL2 (Windows Subsystem for Linux) to provide a full Linux kernel.

https://www.docker.com/products/docker-desktop/

## Container Commands

`docker images`

Returns a complete list of all downloaded images.

`docker pull <image>`

Downloads an image, if no version is specified it downloads the 'latest' version. What Docker does is to download each of the layers that make up the image, if we download another image and its layers have already been installed, those layers will not be installed again, saving time and disk space.

`docker pull <image:version>`

Downloads an image for the specified version.

`docker image rm <image>`

Removes the specified image.

`docker create <image> or docker container create <image>`

Creates a container for the specified image and returns its identifier.

`docker start <containerId> or docker rm <containerName>`

Starts the specified container.

`docker ps`

Lists the running containers.

`docker stop <containerId> or docker rm <containerName>`

Stops the execution of the specified container. When stopped, it is still in a created state, it's just not running.

`docker ps -a`

Lists all containers, even the ones that have been stopped.

`docker rm <containerId> or docker rm <containerName>`

Removes the specified container.

`docker create --name <name> <image>`

Creates a container with a specific name.

`docker create -p<machinePort>:<containerPort> --name <containerName> <image>`

Creates a container for the specified image and maps the container's port to the machine's port. If we don't specify with which machine port it would map, Docker will automatically choose a port.

`docker logs <containerId> or docker logs <containerName>`

Displays the container's logs.

`docker logs --follow <containerId> or docker logs <containerName>`

Displays the container's logs and keeps listening for new logs.

`docker run <image>`

* Checks if the image exists, if not, it downloads it.
* Creates a container.
* Starts the container.

`docker run <image> -d`

Executes the command but in detached mode.

`docker run --name <containerName> -p<machinePort>:<containerPort> -d <image>`

This command creates a new container and assigns it a specific name, maps a specific port of the host machine to a specific port of the container, and runs the container in detached mode.
