# [cite_start]Cloud Computing LAB-4 [cite: 190]

## 🧑‍🎓 Student Details
* **Name:** Vardha Kathura 
* **SRN:** PES1UG23AM343 
* **Section:** F 

## 📌 Overview
This repository contains the advanced Docker lab demonstrating containerization of a Python chat application, message queuing with RabbitMQ, Docker networking, and service orchestration using Docker Compose[cite: 322, 323, 358, 359].

## 📁 Project Files
* `Dockerfile` [cite: 196]
* `chat.py` [cite: 196]
* `docker-compose.yml` [cite: 196]

## 🚀 Execution Steps

### 1. Verification
Verify Docker and Docker Compose installations:

    docker run hello-world [cite: 199]
    docker compose version [cite: 217, 218]

### 2. Build the Application Image
Build the Docker image for the chat application using the provided Dockerfile:

    docker build -t chat-app . [cite: 223]

### 3. Standalone Mode (Container Isolation)
Demonstrate that containers are isolated by default by running the app without a network:

    docker run -d --name rabbitmq rabbitmq:3-management 
    docker run -it --name user-a chat-app 

*(The app falls back to standalone mode because it cannot connect to RabbitMQ at localhost)* 

Clean up before the next step:

    docker rm -f user-a 
    docker stop rabbitmq 
    docker rm rabbitmq 

### 4. Container Communication via Docker Network
Create a user-defined network and attach RabbitMQ:

    docker network create chat-net 
    docker run -d --name rabbitmq --network chat-net rabbitmq:3-management 

[cite_start]Run two chat clients on the same network to enable communication[cite: 322, 323]:

**Terminal 1 (User A)**

    docker run -it --name user-a --network chat-net -e RABBIT_HOST=rabbitmq -e QUEUE_NAME=queue_a -e TARGET_QUEUE=queue_b chat-app 

**Terminal 2 (User B)**

    docker run -it --name user-b --network chat-net -e RABBIT_HOST=rabbitmq -e QUEUE_NAME=queue_b -e TARGET_QUEUE=queue_a chat-app 

### 5. Docker Compose Orchestration
[cite_start]Use the `docker-compose.yml` file to automate the multi-container setup, including RabbitMQ, user-a, user-b, and the chat-net network[cite: 358, 359].

    [cite_start]docker compose up [cite: 358, 359]
