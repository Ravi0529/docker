# Docker Basics 101

A container is an isolated system where users can install/pull required images and work on them.

## Basic Docker Commands

1. `docker container ls`

   - Lists all running containers in Docker.

2. `docker container ls -a`

   - Lists all containers in Docker (running and stopped).

3. `docker start <container_name>`

   - Starts a paused/stopped container.

4. `docker stop <container_name>`

   - Stops a running container.

5. `docker run -it <image_name>`

   - `-it` stands for interactive (connects to container's terminal and keeps connection open)
   - Creates a new container and pulls the image if not already installed locally.

6. `docker exec <container_name> <command_name>`

   - Executes a command in the container from outside.
   - Add `-it` to stay connected to the container.

7. `docker images` or `docker image ls`
   - Lists all images in the local machine.

---

## Port Mapping in Docker

1. `docker run -it -p <host_port>:<container_port> <image_name>`
   - Exposes a port from the Docker container to the local machine.

---

## Passing Environment Variables in Docker

1. `docker run -it -p <port>:<port> -e <key>=<value> <image_name>`
   - Passes environment variables from local machine to the container.

---

## Containerizing Node.js Server with Docker

A `Dockerfile` helps create a custom image of a Node.js server including required packages.

1. `docker build -t <image_name> <Dockerfile_path>`  
   Example: `docker build -t piyush-app .`
   - Creates an image from the configured Dockerfile.

---

## Stacking and Running Multiple Containers in Docker

A `docker-compose.yaml` file creates a stack where multiple containers can run together.

1. Write a docker-compose file as per requirements
2. `docker compose up` (or `docker compose -f <file_name>` for force push)
   - Starts all containers in the stack
3. `docker compose down`
   - Stops the stack
4. `docker compose up -d`
   - Runs the stack in detached mode (background)

---

## Publishing Custom Images on Docker Hub

Steps:

1. Create a repository on Docker Hub (e.g., `piyush-app`)
2. Build a new image with your Docker Hub username and repo name:  
   `docker build -t username/piyush-app .`
3. Push your image to Docker Hub:  
   `docker push username/piyush-app`

---

## Docker Networking

Docker networking enables communication between containers and with the outside world.

1. `docker network ls`

   - Lists all networks in Docker
   - Default networks: `bridge`, `host`, `none`
   - `bridge` is the default network between local machine and containers

2. `docker network inspect bridge`

   - Shows which running containers are connected via bridge network

3. `docker run -it --network=host <image_name>`
   - Changes the container's network from bridge to host

### Network Types:

- **Bridge**: Default (requires port mapping)
- **Host**: Shares host's network (no port mapping needed)
- **None**: No network connection to outside world

---

## Creating Custom Docker Networks

1. `docker network create -d <network_type> <network_name>`  
   Example: `docker network create -d bridge piyush`

### Why create custom networks?

Example:

```bash
docker run -it --network=piyush --name first_container ubuntu
docker run -it --network=piyush --name second_container busybox
```

- Here, busybox and ubuntu are 2 different os running on same network but in different containers, but due to same network, the containers can communicate between one another
