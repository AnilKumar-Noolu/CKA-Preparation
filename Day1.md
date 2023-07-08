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

Kubelet: It runs on every node in the cluster. It eatches for tasks send by api-server and executes them and also reports the status back to manager.
Container runtime : It is a software that runs containers, It can be Docker, containerD or any other tool for containerizing applications.
Kube-proxy: It is a Networking proxy service that runs on ecah node and makes sure that each Node gets and IP to handle the roting, so that we can expose the services to the internet.

## Pods :
             Pod is the smallest and simplest unit in K8 object model. It represents a single instance of running process in a cluster.
1 pod will mostly have  1container
multi container in pods are also supported.
  Commands :  pods ~ po

kubectl get po
kubectl run container-name --image imageName
kubectl apply -f pod.yaml
kubectl get pod -o yaml > pod-definition.yaml
kubectl edit pod
Links : https://kubernetes.io/docs/concepts/workloads/pods/#using-pods

## Replica sets:  
                       Used to make sure that the specific number of replicas are running across all nodes.
Manages node failure
Balances load.
Spread across multiple nodes in the cluster
Has selector label unlike Replication Controller. Selector label allows Replica Set to manage pods which were not created as part of the replica definition file.
It ensures that at all times specified number of pods are available.
Labels and Selectors :

Used to filter or select pods with specific labels. Basically an identifier for pods.
Commands

replicasets ~ rs

kubectl get rs
kubectl apply -f rs.yaml
kubectl replace -f rs.yaml (if count is edited in file)
kubectl scale --replicas=n -f rs.yaml
kubectl delete replicaset rs-name
Links : https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/#example

## Deployments
Encapsulates pod and replica sets. Is used to apply various deployment strategies like rolling updates, blue-green etc.
Very similar to Replica Sets. Apart from RS, deployments can be used to apply updates to running pods like changing image or tag within an image without any downtime.
Commands:

kubectl get all
kubectl get deploy
kubectl apply -f deploy.yaml


## Namespaces
Separates resources eg. Environments
Resources limits like CPU can be set for each namespace
Within Namespace objects are referred directly using the object names
Outside Namespace : svc-name.Namespace.svc.cluster.local
Commands: namespace ~ ns
kubectl create ns namespace1
kubectl get ns
kubectl get po -n namespace1
kubectl get rs -n namespace1




