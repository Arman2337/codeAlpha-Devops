# Task 4: Web Server using Docker

## Overview
This project demonstrates the basics of Docker containerization by creating a simple Nginx web server that serves a static HTML page. It includes health monitoring and utilizes Docker Compose to simplify container lifecycle management.

## Prerequisites
- Docker installed.
- Docker Compose installed.

## Setup Instructions

### 1. Build and Run the Container
To bring up the web server, run:
```bash
docker-compose up -d --build
```
- `up`: Builds, (re)creates, starts, and attaches to containers for a service.
- `-d`: Detached mode (runs the container in the background).
- `--build`: Forces a rebuild of the Docker image before starting.

### 2. Access the Application
Open a web browser and go to `http://localhost:8082`. You should see the welcome page.

### 3. Container Lifecycle Commands
Here are some essential Docker lifecycle commands to manage this container:
- **Check Status**: `docker ps` (Shows running containers. Notice the "healthy" status).
- **View Logs**: `docker logs docker-web-server`
- **Stop Container**: `docker-compose stop`
- **Start Container**: `docker-compose start`
- **Tear Down**: `docker-compose down` (Stops and removes the container and network).

## Monitoring and Health Checks
In the `Dockerfile`, there is a `HEALTHCHECK` directive:
```dockerfile
HEALTHCHECK --interval=30s --timeout=3s \
  CMD wget -qO- http://localhost/ || exit 1
```
This tells Docker to periodically (every 30s) attempt to fetch the homepage. If it fails, Docker marks the container as "unhealthy". This is a critical best practice for containerized applications, as it allows load balancers or orchestrators (like Kubernetes or Docker Swarm) to know if traffic should be routed to this instance.
