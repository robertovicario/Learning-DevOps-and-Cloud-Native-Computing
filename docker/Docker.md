# Docker

## Overview

Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker’s methodologies for shipping, testing, and deploying code quickly, you can significantly reduce the delay between writing code and running it in production.

### Problem: It Works on My Machine

A common issue in software development is the phrase: "It works on my machine". This phrase highlights the inconsistencies that can arise when software behaves differently on different machines or environments. These inconsistencies can stem from differences in operating systems, dependencies, and configurations.

## Dockerfile

A Dockerfile is a text file that contains a series of instructions for building a Docker image. Each instruction in a Dockerfile creates a new layer in the image.

- **Commands:** [docs.docker.com/reference/dockerfile](https://docs.docker.com/reference/dockerfile)

#### Exercise

1. Write a Dockerfile to create an image for a simple Node.js application:

```Dockerfile
# Use an official Node.js runtime as a parent image
FROM node:14

# Set the working directory
WORKDIR /usr/src/app

# Copy the package.json and package-lock.json files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Expose the port the app runs on
EXPOSE 8080

# Command to run the application
CMD ["node", "app.js"]
```

2. Build and run:

```sh
# Build the Docker image
docker build -t my-node-app .

# Run the Docker container
docker run -p 8080:8080 my-node-app
```

### Images

A Docker image is a lightweight, standalone, executable package that includes everything needed to run a piece of software, including the code, runtime, libraries, environment variables, and configuration files. Images are built from a series of layers, with each layer representing a set of file changes or commands.

### Containers

A Docker container is a runnable instance of a Docker image. Containers are isolated from each other and the host system, ensuring that they do not interfere with other containers or the host's environment. This isolation is achieved through technologies such as namespaces and control groups (cgroups).

## Docker Engine

Docker Engine is the core component of Docker, responsible for running and managing Docker containers. It consists of three main parts:

- **Server (dockerd):** A daemon that manages Docker objects (images, containers, networks, volumes) and listens for API requests.

- **REST API:** An interface for interacting with the Docker daemon programmatically.

- **Client (docker):** A command-line tool for interacting with the Docker daemon.

### Architecture

Docker's architecture is based on a client-server model. The key components include:

- **Docker Client:** The primary interface for users to interact with Docker. Commands issued through the Docker Client are sent to the Docker daemon, which carries them out.

- **Docker Daemon:** The background service running on the host machine. It manages Docker objects, such as images, containers, networks, and volumes.

- **Docker Registry:** A centralized repository for storing and distributing Docker images. Public registries like Docker Hub are available, as well as private registries for proprietary images.

- **Docker Objects:** These include images, containers, networks, and volumes, which are created and managed by the Docker daemon.

## Docker Compose

Docker Compose is a tool for defining and running multi-container Docker applications. With Compose, you can use a YAML file to configure your application's services, networks, and volumes. Then, with a single command, you can create and start all the services from your configuration.

- **Commands:** [docs.docker.com/compose/compose-file](https://docs.docker.com/compose/compose-file)

## Volumes

Docker volumes are used to persist data generated and used by Docker containers. Volumes are stored in a part of the host filesystem managed by Docker (`/var/lib/docker/volumes/` on Linux) and are not tied to the lifecycle of a particular container.
