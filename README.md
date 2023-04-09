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

`docker create <image>` or `docker container create <image>`

Creates a container for the specified image and returns its identifier.

`docker start <containerId>` or `docker rm <containerName>`

Starts the specified container.

`docker ps`

Lists the running containers.

`docker stop <containerId>` or `docker rm <containerName>`

Stops the execution of the specified container. When stopped, it is still in a created state, it's just not running.

`docker ps -a`

Lists all containers, even the ones that have been stopped.

`docker rm <containerId>` or `docker rm <containerName>`

Removes the specified container.

`docker create --name <name> <image>`

Creates a container with a specific name.

`docker create -p<machinePort>:<containerPort> --name <containerName> <image>`

Creates a container for the specified image and maps the container's port to the machine's port. If we don't specify with which machine port it would map, Docker will automatically choose a port.

`docker logs <containerId>` or `docker logs <containerName>`

Displays the container's logs.

`docker logs --follow <containerId>` or `docker logs <containerName>`

Displays the container's logs and keeps listening for new logs.

`docker run <image>`

* Checks if the image exists, if not, it downloads it.
* Creates a container.
* Starts the container.

`docker run <image> -d`

Executes the command but in detached mode.

`docker run --name <containerName> -p<machinePort>:<containerPort> -d <image>`

This command creates a new container and assigns it a specific name, maps a specific port of the host machine to a specific port of the container, and runs the container in detached mode.

`docker create -p27017:27017 --name mongoc --network <networkName> -e MONGO_INITDB_ROOT_USERNAME=user -e MONGO_INITDB_ROOT_PASSWORD=password mongo`

This command creates a new Docker container named "mongoc" using the Mongo image, with the environment variables for the root username and password set.

The -p flag maps the container's port 27017 to the host's port 27017. The -e flag sets the environment variables MONGO_INITDB_ROOT_USERNAME and MONGO_INITDB_ROOT_PASSWORD to "user" and "password", respectively.

The --network flag associates the container with the specified network.

`docker network ls`

List the connections available on Docker.

`docker network create <networkName>`

Create a network.

`docker network rm <networkName>`

Deletes a network.

`docker build -t <applicationName>:<version> <currentRoute>`

Creates a Docker container based on a Dockerfile.

## Container networks

Docker networks provide a way for containers to communicate with each other, either on the same host or across different hosts. When multiple containers are running on the same network, they can communicate with each other using their container names as the hostname. This is important because if you want containers to communicate with each other, they must be on the same network. By default, each container runs in its own network namespace, which isolates it from other containers and the host machine. By putting containers on the same network, you allow them to share resources and communicate with each other, making it easier to build complex applications that consist of multiple containers.

## Creating a Docker Container for a Node.js Application

To put a Node.js application inside a Docker container, we need to create a Dockerfile. This file contains instructions for the container to create, and all the images we create must be based on another image.

Here's an example Dockerfile:

```
FROM node:18

RUN mkdir -p /home/app

COPY . /home/app

EXPOSE 3000

CMD ["node", "/home/app/index.js"]
```

This Dockerfile does the following:

- `FROM node:18`: Sets the base image as Node.js version 18.
- `RUN mkdir -p /home/app`: Creates a directory named "app" inside the container at the path "/home".
- `COPY . /home/app`: Copies the current directory (where the Dockerfile is located) into the "/home/app" directory in the container.
- `EXPOSE 3000`: Informs Docker that the application running in the container will listen on port 3000.
- `CMD ["node", "/home/app/index.js"]`: Starts the application inside the container by running the "index.js" file with Node.js.

Once you've created the Dockerfile, you can build the image using the `docker build` command, and then run the container with the `docker run` command.

## Docker Compose

Docker Compose is a tool for defining and running multi-container Docker applications. It allows you to define the services that make up your application in a single YAML file, and then start and stop those services using simple commands. With Docker Compose, you can define the dependencies between your services, map ports and volumes, and configure environment variables and other settings. This makes it easy to develop and deploy complex applications, since you can manage all of the containers in your application as a single entity. Docker Compose is often used in conjunction with Docker Swarm or Kubernetes to orchestrate and manage containerized applications at scale.

### Docker Compose: Configuration File

```yml:title=docker-compose.yml
version: '3'

services:
  db:
    image: postgres

    # Environment variables for the Postgres container.
    environment:
      POSTGRES_USER: myuser
      POSTGRES_PASSWORD: mypassword
      POSTGRES_DB: mydb

    # Expose port 5432 in the container and map it to port 5432 on the host.
    ports:
      - "5432:5432"

  db2:
    image: postgres

    # Environment variables for the second Postgres container.
    environment:
      POSTGRES_USER: myuser
      POSTGRES_PASSWORD: mypassword
      POSTGRES_DB: mydb2

    # Expose port 5432 in the container and map it to port 5433 on the host.
    ports:
      - "5433:5432"
```

### Docker Compose: Commands

`docker compose up`

Starts or creates the containers defined in the `docker-compose.yml` and attaches the terminal to the container output (you can see the logs and the output of every container in the terminal).

If the containers already exist, it starts them without creating them again. If the containers do not exist, it creates and starts them.

If the required image for the services is not available locally Docker Compose will try to pull it from the Docker Hub or the private registry specified in the configuration.

If the command is ran twice without stopping the containers in between, it will end up creating multiple instances of the same container on the same network, which can cause issues like port conflicts, data corruption, and resource utilization problems. It's recommended to run `docker compose up` once and then use other commands like `docker compose stop` and `docker compose start` to manage the containers.

`docker compose up -d`

Starts the containers defined in the `docker-compose.yml` in detached mode.

`docker compose down`

It stops and removes the containers and networks that were created by `docker compose up`, is the opposite of `docker compose up` which starts the containers.

The `--volumes` option also allows to remove the volumes created by the `docker compose up` command.

This command does NOT delete the images downloaded from Docker Hub or other registries.

## Volumes

Until now, whenever we used the `docker compose down` command or the `docker rm <containerName>` command to delete our containers, we inadvertently deleted all the information associated with those file systems.

However, if we want to retain that data, we can use volumes to mount the data into our host file system, thus ensuring that the data is not lost.

Here are some of the main advantages of using volumes:

* Data persistence: Data stored in a Docker volume is persisted on the host machine, even if the container is deleted. This makes it easier to backup and restore data, and ensures that the data is not lost if the container fails or needs to be recreated.

* Sharing data between containers: Multiple containers can share a single volume, making it easier to share data between different services. This is particularly useful when using microservices architecture, where different services need to access the same data.

* Improved performance: Storing data inside a container can lead to performance issues, particularly when the container needs to perform frequent read/write operations. By using a volume, the data is stored outside of the container's writable layer, which can improve performance.

* Easier migration: Docker volumes make it easier to migrate applications between different environments, such as development, testing, and production. Since the data is stored separately from the container, it can be easily moved between different hosts or cloud providers.

There are three types of volumes:

* Anonymous volumes: We only need to specify the path that we want to mount. However, the downside is that we cannot reference these volumes for use in other containers.

* Host volumes: We can specify which folders to mount and where to mount them on the host machine.

* Named volumes: We can assign a name to a volume and reference it from other containers, even after the original container that created the volume has been removed.

### Setting up Volumes on a Docker Compose File

```yml:title=docker-compose.yml
version: '3'

services:
  db:
    image: postgres
    environment:
      POSTGRES_USER: myuser
      POSTGRES_PASSWORD: mypassword
      POSTGRES_DB: mydb

    # Mount a named volume to persist the data in the container.
    volumes:
      - db-data:/var/lib/postgresql/data

    ports:
      - "5432:5432"

  db2:
    image: postgres
    environment:
      POSTGRES_USER: myuser
      POSTGRES_PASSWORD: mypassword
      POSTGRES_DB: mydb2

    # Mount a named volume to persist the data in the container.
    volumes:
      - db2-data:/var/lib/postgresql/data

    ports:
      - "5433:5432"

# Define the named volumes used in the services.
volumes:
  db-data:
  db2-data:
```
