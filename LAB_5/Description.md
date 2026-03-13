# Kubernetes Lab -- Container Orchestration with Minikube

## Overview

This project demonstrates the fundamentals of container orchestration
using **Kubernetes**.\
The lab simulates a "Robot City" where Kubernetes components represent
elements of a city such as districts, citizens, factories, and roads.

Using **Docker, Minikube, and kubectl**, we deploy and manage
containerized applications, perform scaling operations, rolling updates,
and expose services within a Kubernetes cluster.

------------------------------------------------------------------------

## Technologies Used

-   Docker
-   Kubernetes
-   Minikube
-   kubectl
-   Nginx
-   YAML

------------------------------------------------------------------------

## Lab Objectives

This lab demonstrates the following Kubernetes concepts:

-   Creating and managing **Namespaces**
-   Running applications using **Pods**
-   Monitoring pods using **Watch Mode**
-   Debugging using **Logs**
-   Managing applications using **Deployments**
-   **Scaling** applications
-   Performing **Rolling Updates**
-   Deploying applications using **YAML configuration files**
-   Creating **Services** for pod communication
-   **Port forwarding** to access applications locally

------------------------------------------------------------------------

## Project Structure

    .
    ├── html/
    │   └── index.html
    ├── Dockerfile
    ├── nginx-pes1ug23am343.yaml
    ├── pes1ug23am343-service.yaml
    └── README.md

------------------------------------------------------------------------

## Steps Performed

### 1. Start Minikube

    minikube start

### 2. Create Namespaces

    kubectl create namespace pes1ug23am343-alpha
    kubectl create namespace pes1ug23am343-beta

### 3. Create a Pod

    kubectl run citizen --image=nginx --restart=Never

Verify:

    kubectl get pods
    kubectl describe pod citizen

### 4. Watch Mode

    kubectl get pods -w

### 5. View Logs

    kubectl logs citizen

Crash simulation:

    kubectl run broken --image=busybox --restart=Never --command -- sh -c "echo 'CRASH: something went wrong' >&2; exit 1"

### 6. Create Deployment

    kubectl create deployment pes1ug23am343 --image=nginx

Verify:

    kubectl get deployments
    kubectl get pods

### 7. Scaling Deployment

Scale up:

    kubectl scale deployment pes1ug23am343 --replicas=5

Scale down:

    kubectl scale deployment pes1ug23am343 --replicas=3

### 8. Rolling Update

    kubectl set image deployment/pes1ug23am343 nginx=nginx:1.25

### 9. Build Custom Docker Image

    eval $(minikube docker-env)
    docker build -t pes1ug23am343-nginx:1.0 .

### 10. Deploy Using YAML

    kubectl apply -f nginx-pes1ug23am343.yaml -n pes1ug23am343-beta

Verify:

    kubectl get pods

### 11. Create Kubernetes Service

    kubectl apply -f pes1ug23am343-service.yaml

Verify:

    kubectl get services
    kubectl describe service pes1ug23am343-service
    kubectl get endpoints pes1ug23am343-service

### 12. Port Forwarding

    kubectl port-forward deployment/nginx-pes1ug23am343 8080:80

Open in browser:

http://localhost:8080

Expected output:

    Hello from district PES1UG23AM343-beta running in Kubernetes

------------------------------------------------------------------------

## Cleanup

    kubectl delete namespace pes1ug23am343-alpha
    kubectl delete namespace pes1ug23am343-beta

------------------------------------------------------------------------

## Learning Outcomes

Through this lab we learned:

-   How Kubernetes manages containerized applications
-   The role of Pods, Deployments, and Services
-   How scaling and rolling updates work
-   How Kubernetes maintains application availability
-   How to deploy custom container images to a cluster

------------------------------------------------------------------------

## Author

**PES1UG23AM343**\
Computer Science Engineering\
Cloud Computing Lab -- Kubernetes

