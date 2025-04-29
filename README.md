# 📘 Docker Tutorial Summary & Practical Guide

This README provides a summarized guide based on the Docker tutorial covering fundamentals to real-world use. It includes clear explanations, structured learning, and a final project example for applying everything you've learned.

---
# 📌 Introduction to Docker

## 📚 Table of Contents

1. [Introduction to Docker](#-introduction-to-docker)
2. [How to Install Docker](#️-how-to-install-docker)
3. [Common Docker Commands](#-common-docker-commands-with-flags-explained)
4. [Docker Image Layers](#-docker-image-layers)
5. [Port Binding](#-port-binding)
6. [Troubleshooting Docker](#️-troubleshooting-docker)
7. [Docker vs Virtual Machines](#-docker-vs-virtual-machines)
8. [Developing with Docker (Volumes)](#-developing-with-docker-volumes)
9. [Docker Compose](#-docker-compose)
10. [Dockerizing an Application](#-dockerizing-an-application)
11. [Publishing Images to Docker Hub](#-publishing-images-to-docker-hub)
12. [Docker Volumes](#-docker-volumes)

---

# 📌 Introduction to Docker

**Docker** is a platform that uses containerization to package and run applications. A **container** bundles the application code with all its dependencies (libraries, configuration, etc.) into a single, portable unit that runs consistently across environments — from a developer's laptop to production servers.

- Containers are **lightweight**, start quickly, and use **less system resources** compared to traditional virtual machines.
- Docker helps in **CI/CD**, microservices, testing environments, and rapid deployments.

---

# ⚙️ How to Install Docker

1. Go to the official Docker website: [Docker Desktop](https://www.docker.com/products/docker-desktop)
2. Download and install Docker for your operating system (Windows, macOS, or Linux).
3. After installation, verify it works by running:

   ```bash
   docker --version
   ```

---

# 🔧 Common Docker Commands (with flags explained)

| Command                          | Description                                                                 |
|----------------------------------|-----------------------------------------------------------------------------|
| `docker pull <image>`           | Downloads the latest version of an image from Docker Hub.                  |
| `docker run <image>`            | Creates and starts a container using the specified image.                  |
| `docker ps`                     | Lists all **running** containers.                                          |
| `docker ps -a`                  | Lists **all** containers (including stopped ones).                         |
| `docker stop <container_id>`    | Gracefully stops a running container.                                      |
| `docker rm <container_id>`      | Removes a stopped container.                                               |
| `docker images`                 | Lists all downloaded Docker images.                                        |
| `docker rmi <image_id>`         | Deletes a Docker image from your system.                                   |

### Useful flags for `docker run`:
- `-d`: Run container in **detached** mode (in background).
- `-p <host>:<container>`: Map a container port to a port on your host.
- `-v <host_path>:<container_path>`: Mount a volume to persist or share data.
- `--name <name>`: Assign a custom name to your container.
- `-it`: Run the container **interactively** with a terminal (`i = interactive`, `t = terminal`).

Example:
```bash
docker run -d -p 8080:80 --name myweb nginx
```

---

# 🧱 Docker Image Layers

Docker images are built in **layers**, and each instruction in a `Dockerfile` adds a new layer.

Example:
```Dockerfile
FROM node:18          # Base layer with Node.js
WORKDIR /app          # Sets working directory
COPY package.json .   # Copies dependencies file
RUN npm install       # Installs dependencies
COPY . .              # Copies all other app files
CMD ["npm", "start"]  # Runs app on start
```

- **Layer caching** means if a layer hasn’t changed, Docker reuses it to speed up rebuilds.
- Efficient `Dockerfile` structuring = faster builds.

---

# 🌐 Port Binding

Containers are isolated from the host network. Use `-p` to bind ports:
```bash
docker run -p 3000:3000 my-app
```

You can also map different ports:
```bash
docker run -p 8080:3000 my-app
```

---

# 🛠️ Troubleshooting Docker

- View logs of a container:
  ```bash
  docker logs <container_id>
  ```

- Open a shell inside a running container:
  ```bash
  docker exec -it <container_id> bash
  ```

- Clean up unused containers, networks, and volumes:
  ```bash
  docker container prune
  ```

---

# 🧦 Docker vs Virtual Machines

| Feature             | Docker Containers                | Virtual Machines             |
|---------------------|----------------------------------|------------------------------|
| Resource Usage       | Lightweight                      | Heavy (full OS per VM)       |
| Boot Time           | Seconds                          | Minutes                      |
| OS Overhead         | Shares host OS kernel            | Requires full OS             |
| Portability         | High                             | Medium                       |
| Use Case            | Microservices, CI/CD, DevOps     | Legacy apps, full isolation  |

---

# 💻 Developing with Docker (Volumes)

Use **volumes** to sync your source code with the container:
```bash
docker run -v $(pwd):/app -p 3000:3000 node
```

This:
- Mounts current working directory (`$(pwd)`) to `/app` inside container
- Enables live-reloading or changes without rebuilding the container

---

# 🧹 Docker Compose

**Docker Compose** manages multi-container applications using a YAML file.

Example `docker-compose.yml`:
```yaml
version: '3'
services:
  web:
    build: ./app
    ports:
      - "3000:3000"
  db:
    image: mongo
    ports:
      - "27017:27017"
```

Run with:
```bash
docker-compose up
```

---

# 🐋 Dockerizing an Application

Steps to Dockerize a Node.js app:

1. Create `Dockerfile`:
   ```Dockerfile
   FROM node:18
   WORKDIR /app
   COPY . .
   RUN npm install
   EXPOSE 3000
   CMD ["npm", "start"]
   ```

2. Build the image:
   ```bash
   docker build -t myapp .
   ```

3. Run the container:
   ```bash
   docker run -p 3000:3000 myapp
   ```

---

# 🚀 Publishing Images to Docker Hub

1. Log in:
   ```bash
   docker login
   ```

2. Tag your image:
   ```bash
   docker tag myapp yourusername/myapp
   ```

3. Push it:
   ```bash
   docker push yourusername/myapp
   ```

Other users can now pull it using:
```bash
docker pull yourusername/myapp
```

---

# 💾 Docker Volumes

Volumes store data **outside** the container's lifecycle, so data is preserved even after a container is deleted.

1. Create a volume:
   ```bash
   docker volume create mydata
   ```

2. Mount it into a container:
   ```bash
   docker run -v mydata:/data myapp
   ```

3. To inspect volume:
   ```bash
   docker volume inspect mydata
   ```

4. To remove unused volumes:
   ```bash
   docker volume prune
   ```

---


## 🧪 Project Example: MERN Stack in Docker

**Project Structure:**

```
project/
├── docker-compose.yml
├── backend/
│   └── Dockerfile
├── frontend/
│   └── Dockerfile
```

### 🐋 docker-compose.yml

```yaml
version: '3.8'
services:
  mongo:
    image: mongo
    ports:
      - "27017:27017"

  backend:
    build: ./backend
    ports:
      - "5000:5000"
    environment:
      MONGO_URI: mongodb://mongo:27017/mydb
    depends_on:
      - mongo

  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
```

### 🛠 backend/Dockerfile

```Dockerfile
FROM node:18
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 5000
CMD ["npm", "run", "dev"]
```

### 🎨 frontend/Dockerfile

```Dockerfile
FROM node:18
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 3000
CMD ["npm", "start"]
```

### 🚀 Run the whole app

```bash
docker-compose up --build
```

---

## 🎉 Conclusion

This tutorial takes you from understanding Docker basics to building and deploying a real-world MERN application using containers. You now know how to:

- Use Docker CLI and Dockerfiles
- Connect multiple services with Docker Compose
- Share your images via Docker Hub
- Persist data using volumes



