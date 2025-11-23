#docker #skillsheet
___
### Image Management
```shell
docker pull <image>:<tag>
docker images
docker image prune            # Remove dangling images
docker rmi <image_name>
docker build -t <image_name:tag> .
docker push <username>/<repository>:<tag>
docker history <image>        # Show image build history
```

### Container Lifecycle
```shell
docker run <image>:<tag>
docker run -d <image>:<tag>
docker run -d -p <host_port>:<container_port> <image>:<tag>
docker run --name <container_name> -d -p <host_port>:<container_port> <image>:<tag>
docker run -v $(pwd):/app <image>:<tag>   # Mount current directory
docker ps
docker ps -a
docker stop <container_name_or_id>
docker start <container_name_or_id>
docker rm <container_name_or_id>
docker rm -f <container_name_or_id>
```

### Container Interaction
```shell
docker logs <container_name_or_id>
docker exec -it <container_name_or_id> <command>
docker inspect <container_name_or_id>
docker stats                  # Show container resource usage
docker rename <old> <new>     # Rename a container
```

### Networking
```shell
docker network ls
docker network create <network_name>
docker network connect <network_name> <container_name_or_id>
docker network disconnect <network_name> <container_name_or_id>
```

### Volumes
```shell
docker volume create <volume_name>
docker run -v <volume_name>:<container_path> <image>
docker volume ls
docker volume rm <volume_name>
docker volume inspect <volume_name>
docker cp <container_name>:<path_inside_container> ./backup  # Copy data out safely
docker volume prune

```

### Docker Compose
```shell
docker-compose up -d
docker-compose down
docker-compose ps
docker-compose logs
```

### System Maintenance
```shell
docker system prune
docker system df    # Shows Docker container Disk Usage
docker info
```

### Notes:
- When using `docker run`, it will pull the image if it doesn't exist locally.
- The `-d` flag detaches the container, running it in the background.
- Port mapping is done with `-p host_port:container_port`.
- Use `--name` to specify a custom name for a container.
- The `-f` flag with `docker rm` forces removal of a running container.
- Use `docker exec` to run commands in a running container.
- `docker compose` is used for managing multi-container applications.
	- Note: This should be the default to lean in to. See [[Minecraft-Docker-Compose]] as an example.
- `docker system prune` removes unused Docker objects to free up space.
