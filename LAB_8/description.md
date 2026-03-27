# Raft Consensus Algorithm using Docker

A distributed systems lab that demonstrates the Raft consensus algorithm running across multiple Docker containers. Nodes communicate over a shared network to elect a leader, maintain log consistency, and recover from failures automatically.

---

## Table of Contents

- [Overview](#overview)
- [Objectives](#objectives)
- [Project Structure](#project-structure)
- [Requirements](#requirements)
- [Setup](#setup)
- [Running the Project](#running-the-project)
- [Observing Behavior](#observing-behavior)
- [Simulating Fault Tolerance](#simulating-fault-tolerance)
- [Stopping the System](#stopping-the-system)
- [Results](#results)
- [Conclusion](#conclusion)

---

## Overview

This project spins up three Docker containers, each acting as an independent Raft node. The nodes discover each other through Docker's internal DNS, conduct an election, and continuously report their role. If the current leader is stopped, the remaining nodes hold a new election and a replacement leader is chosen without any manual intervention.

---

## Objectives

- Understand the fundamentals of distributed consensus
- Study the Raft algorithm in a hands-on environment
- Use Docker and Docker Compose to simulate a multi-node cluster
- Observe leader election, follower behavior, and log replication
- Demonstrate automatic recovery after node failure
- Understand Docker networking in the context of distributed systems

---

## Project Structure

```
raft-docker-lab/
├── node.py
├── Dockerfile
├── docker-compose.yml
└── requirements.txt
```

---

## Requirements

- Docker (installed and running)
- Docker Compose v2 or later
- Linux, Ubuntu, or WSL terminal

---

## Setup

### 1. Create the Project Directory

```bash
mkdir raft-docker-lab
cd raft-docker-lab
```

### 2. Create the Required Files

```bash
touch node.py Dockerfile requirements.txt docker-compose.yml
```

### 3. requirements.txt

```
raftos
```

### 4. Dockerfile

```dockerfile
FROM python:3.10
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
CMD ["python", "node.py"]
```

### 5. docker-compose.yml

```yaml
version: '3'
services:
  node1:
    build: .
    container_name: node1
    ports:
      - "8001:8000"

  node2:
    build: .
    container_name: node2
    ports:
      - "8002:8000"

  node3:
    build: .
    container_name: node3
    ports:
      - "8003:8000"
```

### 6. node.py

```python
import raftos
import asyncio
import os

node_id = os.getenv("HOSTNAME")

async def main():
    await raftos.register(
        address=node_id,
        cluster=[
            "node1:8000",
            "node2:8000",
            "node3:8000"
        ]
    )

    while True:
        if raftos.get_leader() == node_id:
            print(f"[LEADER {node_id}] I am the leader")
        else:
            print(f"[FOLLOWER {node_id}] Current leader: {raftos.get_leader()}")

        await asyncio.sleep(2)

if __name__ == "__main__":
    asyncio.run(main())
```

---

## Running the Project

Build and start all three nodes:

```bash
docker compose up --build
```

Docker will build the image, create the containers, and connect them on a shared network. The nodes will begin the election process automatically once they are all running.

---

## Observing Behavior

### View Logs for Each Node

```bash
docker logs -f node1
docker logs -f node2
docker logs -f node3
```

One node will print `[LEADER ...]` while the others print `[FOLLOWER ...]` along with the name of the current leader.

### List Running Containers

```bash
docker ps
```

### Inspect the Docker Network

```bash
docker network inspect raft-docker-lab_raftnet
```

This shows the internal IP addresses and network configuration used by the nodes to communicate.

---

## Simulating Fault Tolerance

### Stop the Leader Node

```bash
docker stop node2
```

The two remaining nodes detect the absence of the leader, trigger a new election, and one of them is promoted to leader. This happens automatically within the election timeout period defined by the Raft protocol.

### Restart the Stopped Node

```bash
docker start node2
```

The restarted node rejoins the cluster as a follower and begins syncing state from the current leader.

---

## Stopping the System

```bash
docker compose down
```

This stops and removes all containers, networks, and volumes created by Compose.

---

## Results

The system successfully demonstrates:

- Automatic leader election among three nodes using the Raft protocol
- Continuous role reporting from each node via container logs
- Fault detection and re-election when the current leader is stopped
- Seamless node rejoin as a follower after being restarted

---

## Conclusion

This project provides a practical introduction to distributed consensus through the Raft algorithm. By running each node as an isolated Docker container on a shared network, the setup closely mirrors real-world distributed deployments. The experiment confirms that Raft reliably maintains cluster consistency and leadership continuity even in the presence of node failures, making it a strong foundation for understanding fault-tolerant distributed systems.
