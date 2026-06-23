# Docker Basic Commands Cheat Sheet

## 1. Docker Images Commands

| Command                        | Description                       |
| ------------------------------ | --------------------------------- |
| `docker images`                | Show all Docker images            |
| `docker pull image_name`       | Download an image from Docker Hub |
| `docker build -t image_name .` | Create image from Dockerfile      |
| `docker rmi image_name`        | Remove an image                   |
| `docker rmi IMAGE_ID`          | Remove image using ID             |
| `docker image prune`           | Remove unused images              |
| `docker image prune -a`        | Remove all unused images          |

---

## 2. Docker Container Commands

| Command                         | Description                             |
| ------------------------------- | --------------------------------------- |
| `docker ps`                     | Show running containers                 |
| `docker ps -a`                  | Show all containers (running + stopped) |
| `docker run image_name`         | Create and run a new container          |
| `docker run -d image_name`      | Run container in background mode        |
| `docker stop container_name`    | Stop a running container                |
| `docker start container_name`   | Start stopped container                 |
| `docker restart container_name` | Restart container                       |
| `docker rm container_name`      | Remove container                        |
| `docker rm -f container_name`   | Force remove running container          |
| `docker container prune`        | Remove all stopped containers           |
| `docker logs container_name`    | Show container logs                     |
| `docker logs -f container_name` | Show live logs                          |

---

## 3. Docker Exec Commands

| Command                              | Description                        |
| ------------------------------------ | ---------------------------------- |
| `docker exec -it container_name sh`  | Enter inside container shell       |
| `exit`                               | Exit from container shell          |

Example:

```bash
docker exec -it pet-server sh
```

---

## 4. Docker Volume Commands

| Command                              | Description                         |
| ------------------------------------ | ----------------------------------- |
| `docker volume ls`                   | Show all Docker volumes             |
| `docker volume create volume_name`   | Create a new volume                 |
| `docker volume inspect volume_name`  | Show volume details                 |
| `docker volume rm volume_name`       | Remove a volume                     |
| `docker volume prune`                | Remove all unused volumes            |

Example:

```bash
docker volume create pet-volume
```

---



## 5. Docker Network Commands

| Command                                  | Description                          |
| ---------------------------------------- | ------------------------------------ |
| `docker network ls`                      | Show all Docker networks             |
| `docker network create network_name`     | Create a new network                 |
| `docker network inspect network_name`    | Show network details                 |
| `docker network rm network_name`         | Remove a network                     |
| `docker network prune`                   | Remove unused networks               |

Example:

Create network:

```bash
docker network create pet-network
```


