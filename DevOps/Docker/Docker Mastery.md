## Index
[[#Install]]
[[#Basics]]
[[#Monitoring]]
[[#Get inside with Shell]]
[[#Networks]]

---
---
---
### References
[Play with Docker](https://labs.play-with-docker.com)
[Training with Docker](https://training.play-with-docker.com)
[Docker docs](https://docs.docker.com)

---
### Install
```shell
# Linux
curl -sSL https://get.docker.com/ | sh

# Start on boot
sudo systemctl enable docker
sudo systemctl enable containerd

# Run docker commands without sudo
sudo usermod -aG docker $USER
# Activate the changes to groups
newgrp docker
```

---
### Basics

>[!info] Command line structure
>`docker <command> <sub-command> (options)`

```shell
docker version
# more info about Docker
docker info

# Commands that I can use
docker
# Alternative
docker --help
```

Example starting a Nginx container:
```shell
# Download nginx image
# Start a new container from the image
# Open port 80
# Routes that traffic to the container, port 80 
docker container run --publish 80:80 nginx
```

>[!tip] Ports
>You can use any port you want on the left, then use `externalport:internalport` when testing.

>[!danger] If you're using WSL...
>Remember to check the IP address with the `hostname -I` command.

```shell
# Run container in the background
docker container run --publish 80:80 --detach nginx
# You can set a name to the container
docker container run --publish 80:80 --name webhost --detach nginx

# List running containers
docker container ls

# List ALL containers available
docker container ls -a

# Stop a running container
docker container stop <container_id/name>

# Start a stopped container
docker container start <container_id/name>

# Check the logs
docker container logs <container_id/name>

# To check the process running
docker container top <container_id/name>

# To check the options in the container command
docker container --help

# To remove a stopped container
docker container rm <container_id/name>

# Or you can force to remove a running container
docker container rm -f <container_id/name>
```

>[!tip] Container ID
>You can indicate the container ID with the first 3 characters or digits.

>[!danger] The importance of **learning Linux**
>Most of Docker's commands are Linux based.
>So, knowing Linux might make the learning path easier.

---
### Monitoring
```shell
# Process list in one container
docker container top <id/name>

# Details of one container config
docker container inspect <id/name>

# Performance stats for all containers
docker container stats
```

---
### Get inside with Shell
```shell
# Start new container interactively
docker container run -it --name name <image> bash
```

>[!info] Be careful with the `-it` command!
>If you use it to run a new container, once you quit the container, it'll stop!

```shell
# Run additional command in existing container
docker container exec -it <id/name> bash

# If the container is an OS like Ubuntu
docker container start -it <id/name>

# Or with Alpine Linux
docker container run -it alpine sh
```

---
### Networks
Containers can talk to each other with the same virtual network. Example:
- network "my_web_app" for mysql and php/apache containers.

In some cases, you might need to skip virtual networks and use host IP with `--net=host`

```shell
# Which ports are forwarding traffic to the container.
docker container port <id/name>

# To check the IP address of the container
docker container inspect --format "{{.NetworkSettings.IPAddress}}" <id/name>

# Show networks
docker network ls

# Inspect a network - like which containers are attached
docker network inspect <network-name>

# Create a network
docker network create <name>
docker network create --driver

# Dynamically adds a NIC from a container on a specific virtual network
docker network connect <virtual_net> <container>

# Dynamically removes a NIC from a container on a specific virtual network
docker network disconnect <container> <virtual_net>
```

>[!info] Different interfaces
>`bridge` - It's default Docker virtual network, which is NAT'ed behind the host IP.
>`host` - It gains performance by skipping virtual networks but sacrifices security of container model.
>`none` - removes eth0 and only leaves you with localhost interface in container.

>[!info] Network DRIVER
>Built-in or 3rd party extensions that give you virtual network features.

