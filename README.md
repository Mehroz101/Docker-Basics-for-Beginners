# Docker Basics for Beginners

Welcome! This guide explains the **essential Docker commands** in a very simple way for beginners.

---

## What is Docker?

- Docker lets you create "containers".
- A container is like a mini-computer that runs your app anywhere, without problems.

---

# Install Docker

- Download and install Docker Desktop from [https://www.docker.com/products/docker-desktop/](https://www.docker.com/products/docker-desktop/)
- After installation, open your terminal or command prompt.

---

# Basic Docker Commands

## 1. Check if Docker is working

```bash
docker --version
```

Shows the installed Docker version.

---

## 2. Pull an image (download)

```bash
docker pull IMAGE_NAME
```

Example:

```bash
docker pull nginx
```

This downloads the **nginx** server image.

---

## 3. See downloaded images

```bash
docker images
```

Lists all images you have downloaded.

---

## 4. Run a container

```bash
docker run IMAGE_NAME
```

Example:

```bash
docker run nginx
```

Runs the nginx server.

To keep the container running in the background (detached mode):

```bash
docker run -d nginx
```

---

## 5. See running containers

```bash
docker ps
```

Lists only running containers.

To see **all** containers (including stopped ones):

```bash
docker ps -a
```

---

## 6. Stop a running container

```bash
docker stop CONTAINER_ID
```

Example:

```bash
docker stop abc123
```

(Use `docker ps` to find the `CONTAINER_ID`.)

---

## 7. Remove a container

```bash
docker rm CONTAINER_ID
```

Deletes the container.

---

## 8. Remove an image

```bash
docker rmi IMAGE_NAME
```

Deletes an image.

---

# Extra Useful Commands

## Run a container with port mapping

```bash
docker run -d -p HOST_PORT:CONTAINER_PORT IMAGE_NAME
```

Example:

```bash
docker run -d -p 8080:80 nginx
```

Now you can access nginx at `http://localhost:8080`

---

## Build your own image

If you have a `Dockerfile`:

```bash
docker build -t YOUR_IMAGE_NAME .
```

---

# Helpful Tips

- `docker stop $(docker ps -q)` — Stops all running containers.
- `docker rm $(docker ps -a -q)` — Removes all containers.
- `docker rmi $(docker images -q)` — Removes all images.

---

# Final Words

Docker is super powerful, but start slow. First, practice pulling images and running containers.

> "Build small containers, and grow your confidence!"

---

# Happy Dockering! 🌊

If you want more beginner projects with Docker, let me know!

