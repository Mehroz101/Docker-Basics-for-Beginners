# 🐳 Beginner's Guide to Docker (With MERN Example)

This guide will help you learn Docker from **zero** to **hero** in the simplest way — whether you’re a MERN stack developer or working with any other tech stack!

---

## 📦 What is Docker?

Docker is a tool that helps you **package** your application and everything it needs (like libraries, system tools) into one **container** — so it works the same on any computer.

Think of it as a box 📦 for your app.

---

## 🚀 Common Docker Commands

| Command | Description |
|--------|-------------|
| `docker --version` | Check Docker version |
| `docker pull IMAGE_NAME` | Download an image from Docker Hub |
| `docker images` | List all downloaded images |
| `docker ps` | List running containers |
| `docker ps -a` | List all containers (running and stopped) |
| `docker run IMAGE_NAME` | Run a container from an image |
| `docker stop CONTAINER_ID` | Stop a container |
| `docker rm CONTAINER_ID` | Remove a container |
| `docker rmi IMAGE_ID` | Remove an image |

---

## 📥 Pulling an Image

```bash
docker pull node
```
This command pulls the official **Node.js** image.

---

## 📦 Creating and Running a Container

```bash
docker run -d -p 3000:3000 node
```
- `-d`: Run in background
- `-p`: Map port 3000 from container to local machine

---

## 🔧 Building Your Own Docker Image

1. Create a `Dockerfile` in your project root:

```Dockerfile
FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
```

2. Build the image:
```bash
docker build -t my-mern-app .
```

3. Run it:
```bash
docker run -d -p 3000:3000 my-mern-app
```

---

## 🪝 Push Your Image to Docker Hub

1. Login:
```bash
docker login
```

2. Tag your image:
```bash
docker tag my-mern-app username/my-mern-app
```

3. Push it:
```bash
docker push username/my-mern-app
```

---

## 🌐 Docker Networks

To let containers talk to each other:

```bash
docker network create my-network
```

Run containers inside the network:
```bash
docker run -d --network my-network --name backend backend-image
```
```bash
docker run -d --network my-network --name frontend frontend-image
```

They can now communicate using container names.

---

## 📄 docker-compose.yml — Running Multiple Containers

Use `docker-compose` to run multiple containers easily. Example with MERN (MongoDB + Express + React + Node):

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
    depends_on:
      - mongo

  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
```

Run with:
```bash
docker-compose up --build
```

Stop with:
```bash
docker-compose down
```

---

## 🧠 Understanding the Folders (MERN Example)

```
project-root/
├── docker-compose.yml
├── frontend/
│   ├── Dockerfile
│   └── ...
├── backend/
│   ├── Dockerfile
│   └── ...
```

### Example Frontend Dockerfile (React)
```Dockerfile
FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
```

### Example Backend Dockerfile (Express)
```Dockerfile
FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 5000
CMD ["npm", "start"]
```

---

## 🧾 .dockerignore (Optional but Recommended)

This file tells Docker what NOT to copy when building.

```
node_modules
.env
.git
```

---

## ✅ Final Tips

- Use Docker when you want consistency across different machines.
- Docker Compose is your friend for full-stack apps.
- Push your image to Docker Hub to share it.

---

## 🔚 You're Ready!

You now know how to:
- Pull and run images
- Create containers
- Write Dockerfiles
- Use Docker Compose to run multiple services
- Push your own image to Docker Hub

Happy Dockering! 🐳✨

