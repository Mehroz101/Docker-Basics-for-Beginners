# 📘 Docker Tutorial Summary & Practical Guide

This README provides a summarized guide based on the Docker tutorial covering fundamentals to real-world use. It includes clear explanations, structured learning, and a final project example for applying everything you've learned.

---

## 🧠 Table of Contents

1. [Introduction to Docker](#introduction-to-docker)
2. [Installing Docker](#installing-docker)
3. [Essential Docker Commands](#essential-docker-commands)
4. [Understanding Docker Image Layers](#docker-image-layers)
5. [Port Binding Explained](#port-binding)
6. [Troubleshooting with Logs](#troubleshooting)
7. [Docker vs Virtual Machines](#docker-vs-virtual-machines)
8. [Developing with Docker](#developing-with-docker)
9. [Docker Compose](#docker-compose)
10. [Dockerizing an Application](#dockerizing-an-application)
11. [Publishing to Docker Hub](#publishing-to-docker-hub)
12. [Working with Volumes](#docker-volumes)
13. [Project Example: MERN Stack in Docker](#project-example)

---

## 📌 Introduction to Docker&#x20;

Docker is a containerization platform that lets developers package applications with all dependencies into standardized units — called containers. Containers ensure consistency across development, testing, and production environments.

---

## ⚙️ Installing Docker&#x20;

1. Visit [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)
2. Install Docker Desktop for your OS (Windows/Mac/Linux)
3. Verify installation:
   ```bash
   docker --version
   ```

---

## 🔧 Essential Docker Commands

| `docker pull <image>` | Download an image       |
| --------------------- | ----------------------- |
| `docker run <image>`  | Run a container         |
| `docker ps`           | List running containers |
| `docker ps -a`        | List all containers     |
| `docker stop <id>`    | Stop a container        |
| `docker rm <id>`      | Remove container        |
| `docker images`       | List images             |
| `docker rmi <id>`     | Remove image            |

---

## 🧱 Docker Image Layers&#x20;

Every instruction in a `Dockerfile` creates a layer. Layers are reused to optimize builds. For example:

```Dockerfile
FROM node:18       # Layer 1
WORKDIR /app       # Layer 2
COPY package.json . # Layer 3
RUN npm install    # Layer 4
```

Each step saves time during rebuilds by caching unchanged layers.

---

## 🌐 Port Binding&#x20;

Containers run in isolation, so you must bind internal ports to host ports:

```bash
docker run -p 3000:3000 my-app
```

This exposes container port 3000 to your machine’s port 3000.

---

## 🛠️ Troubleshooting View logs:

-
  ```bash
  docker logs <container_id>
  ```
- Enter running container:
  ```bash
  docker exec -it <container_id> bash
  ```
- Remove stuck containers:
  ```bash
  docker container prune
  ```

---

## 🆚 Docker vs Virtual Machines&#x20;

| Docker Containers | Virtual Machines   |
| ----------------- | ------------------ |
| Lightweight       | Heavy              |
| Fast boot times   | Slow boot          |
| Shares OS kernel  | Requires full OS   |
| Better for DevOps | Used for isolation |

---

## 💻 Developing with Docker&#x20;

Mount your code into containers using **volumes**:

```bash
docker run -v $(pwd):/app -p 3000:3000 node
```

This keeps your live code synced with the container.

---

## 🧩 Docker Compose&#x20;

Compose lets you define multiple services in a single YAML file.
Example:

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

Run it:

```bash
docker-compose up
```

---

## 🐳 Dockerizing an Application&#x20;

1. Create `Dockerfile`:
   ```Dockerfile
   FROM node:18
   WORKDIR /app
   COPY . .
   RUN npm install
   EXPOSE 3000
   CMD ["npm", "start"]
   ```
2. Build:
   ```bash
   docker build -t myapp .
   ```
3. Run:
   ```bash
   docker run -p 3000:3000 myapp
   ```

---

## 🚀 Publishing Images to Docker Hub

1. Login:
   ```bash
   docker login
   ```
2. Tag image:
   ```bash
   docker tag myapp username/myapp
   ```
3. Push:
   ```bash
   docker push username/myapp
   ```

---

## 💾 Docker Volumes&#x20;

Volumes persist data outside the container lifecycle:

```bash
docker volume create mydata
```

Mount it:

```bash
docker run -v mydata:/data myapp
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



