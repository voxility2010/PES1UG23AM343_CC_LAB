# [cite_start]Cloud Computing LAB-4 [cite: 190]

## 🧑‍🎓 Student Details
* [cite_start]**Name:** Vardha Kathura [cite: 191]
* [cite_start]**SRN:** PES1UG23AM343 [cite: 191]
* [cite_start]**Section:** F [cite: 191]

## 📌 Overview
[cite_start]This repository contains the advanced Docker lab demonstrating containerization of a Python chat application, message queuing with RabbitMQ, Docker networking, and service orchestration using Docker Compose[cite: 322, 323, 358, 359].

## 📁 Project Files
* [cite_start]`Dockerfile` [cite: 196]
* [cite_start]`chat.py` [cite: 196]
* [cite_start]`docker-compose.yml` [cite: 196]

## 🚀 Execution Steps

### 1. Verification
[cite_start]Verify Docker and Docker Compose installations[cite: 192, 213]:

    docker run hello-world [cite: 199]
    docker compose version [cite: 217, 218]

### 2. Build the Application Image
[cite_start]Build the Docker image for the chat application using the provided Dockerfile[cite: 221]:

    docker build -t chat-app . [cite: 223]

### 3. Standalone Mode (Container Isolation)
[cite_start]Demonstrate that containers are isolated by default by running the app without a network[cite: 257, 258]:

    docker run -d --name rabbitmq rabbitmq:3-management [cite: 226]
    docker run -it --name user-a chat-app [cite: 261]

[cite_start]*(The app falls back to standalone mode because it cannot connect to RabbitMQ at localhost)* [cite: 283, 285, 289]

[cite_start]Clean up before the next step[cite: 299, 300]:

    docker rm -f user-a [cite: 302]
    docker stop rabbitmq [cite: 308]
    docker rm rabbitmq [cite: 309]

### 4. Container Communication via Docker Network
[cite_start]Create a user-defined network and attach RabbitMQ[cite: 304, 305]:

    docker network create chat-net [cite: 307]
    docker run -d --name rabbitmq --network chat-net rabbitmq:3-management [cite: 310]

[cite_start]Run two chat clients on the same network to enable communication[cite: 322, 323]:

**Terminal 1 (User A)**

    docker run -it --name user-a --network chat-net -e RABBIT_HOST=rabbitmq -e QUEUE_NAME=queue_a -e TARGET_QUEUE=queue_b chat-app [cite: 325]

**Terminal 2 (User B)**

    docker run -it --name user-b --network chat-net -e RABBIT_HOST=rabbitmq -e QUEUE_NAME=queue_b -e TARGET_QUEUE=queue_a chat-app [cite: 340, 341, 342]

### 5. Docker Compose Orchestration
[cite_start]Use the `docker-compose.yml` file to automate the multi-container setup, including RabbitMQ, user-a, user-b, and the chat-net network[cite: 358, 359].

    [cite_start]docker compose up [cite: 358, 359]
