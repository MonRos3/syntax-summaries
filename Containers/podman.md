# Podman Commands

Podman commands can be used in place of docker commands. It can also fetch and use docker images.

## Machine Management

Initialize and start a Podman machine (primarily for macOS and Windows):

```bash
podman machine init
```

```bash
podman machine start
```

```bash
podman machine stop
```

```bash
podman machine list
```

OR

```bash
podman ps -a
```

## Container Management

### Running Containers

```bash
# Run a container interactively
podman run -it ubuntu bash

# Run a container in detached mode
podman run -d nginx

# Run with port mapping
podman run -p 8080:80 nginx

# Run with volume mount
podman run -v /host/path:/container/path alpine
```

### Container Lifecycle

```bash
# List running containers
podman ps

# List all containers (including stopped)
podman ps -a

# Stop a container
podman stop <container_id>

# Start a stopped container
podman start <container_id>

# Restart a container
podman restart <container_id>

# Remove a container
podman rm <container_id>

# Remove all stopped containers
podman container prune
```

### Container Inspection

```bash
# View container logs
podman logs <container_id>

# Execute commands in running container
podman exec -it <container_id> bash

# Inspect container details
podman inspect <container_id>

# View container resource usage
podman stats
```

## Image Management

### Working with Images

```bash
# Pull an image from registry
podman pull nginx

# List local images
podman images

# Remove an image
podman rmi <image_id>

# Remove unused images
podman image prune

# Build image from Dockerfile
podman build -t myapp .

# Tag an image
podman tag <image_id> myrepo/myapp:latest
```

### Registry Operations

```bash
# Push image to registry
podman push myrepo/myapp:latest

# Search for images
podman search nginx

# Login to registry
podman login docker.io
```

## Pod Management

Podman's unique feature - managing groups of containers:

```bash
# Create a pod
podman pod create --name mypod

# Run container in a pod
podman run -dt --pod mypod nginx

# List pods
podman pod list

# Stop a pod
podman pod stop mypod

# Remove a pod
podman pod rm mypod
```

## Volume Management

```bash
# Create a volume
podman volume create myvolume

# List volumes
podman volume ls

# Remove a volume
podman volume rm myvolume

# Remove unused volumes
podman volume prune
```

## Network Management

```bash
# List networks
podman network ls

# Create a network
podman network create mynetwork

# Remove a network
podman network rm mynetwork

# Run container with specific network
podman run --network mynetwork nginx
```

## System Commands

```bash
# Show system information
podman info

# Show version
podman version

# Clean up unused resources
podman system prune

# Show disk usage
podman system df
```
