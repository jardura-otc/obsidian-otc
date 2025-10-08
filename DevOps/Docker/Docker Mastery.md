## Index


---
---
---
### References
[Play with Docker](https://labs.play-with-docker.com)
[Training with Docker](https://training.play-with-docker.com)
[Docker docs](https://docs.docker.com)

---
### Roadmap
- [ ] Requirements
- [ ] Docker Install
- [ ] Container Basics
- [ ] Image Basics
- [ ] Docker Networking
- [ ] Docker Volumes
- [ ] Docker Compose
- [ ] Orchestration
	- [ ] Docker Swarm
	- [ ] Kubernetes

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

