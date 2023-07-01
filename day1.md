## Day 1

## Core Concepts

Learnt about basics of Docker like creating a Dockerfile and building it to an image and start running containers based on that image.

Had a look on Other containerization tools like ContainerD, crictl and difference between them and Docker

## Kubernetes Architecture

Kubernetes is an open-source system for automating deployment, scaling and management of containerized applications. Kuberenetes is managed by Cloyud Native Computing Foundation(CNCF).
One of the key componenetas of K8 is it can run applications on cluster of physical machines and VM infrastructure. It also has capability to run applications on cloud. Helps in moving from Host-Centric to container-centric infrastructure.

## Master Node:

Responsible for scheduling deployments and management of Kubernetes Cluster. Acts as an entry point for all administrative tasks.
 ## Components:

Api Server : front end that users and cmd can talk to or use to communicate with the cluster
etcd : Distributed key value storage which stores all information of the K8 cluster
Scheduler : Regulates the tasks by scheduling work on containers across Worker nodes.
Controller : brain behind K8, notices when a node is down , takes desicions to bring up new containers

## Worker Node:
Nodes are workhorses of K8 Cluster. Nodes expose Compute, Networking and Storage.
## Components:

kubelet: It runs on every node in the cluster. It eatches for tasks send by api-server and executes them and also reports the status back to manager
