## Storage
There are mainly 2 concepts of storage in Docker i.e. 1)Storage Driver, 2)Volume Driver
## Storage Driver:
Storage driver help manage storage on images and containers.

By default, Docker stores its file in default folder /var/lib/docker. In Docker, there are 2 types of mounting.
1. Volume Mount: It mounts a volume from the volume directory.
    ` docker run -v data-vol:/var/lib/mysql mysql`
2. Bind Mount: It mounts a directory from any location on the DockerHost.
    ` docker run -v /data/mysql:/var/lib/mysql mysql`

3. New way of mounting the storage: `docker run --mount type=bind, source=/data/mysql, target=/var/lib/mysql mysql`

Storage Drivers is responsible for doing all these operations. Ex: Maintaining layeres architecture, moving files across layers to copy,..

Common Storage drivers include AUFS, ZFS, BTRFS, Device Mapper, Overlay1, ..

## Volume Drivers:
If you want to persist storage, you must create volumes. These volumes are handled by Volume Driver.

When you run Docker Container, you can choose to use a specific volume driver such as REX-Ray, EBS to provision AWS EBS.
` docker run -it name mysql 
        --volume-driver rexray/ebs
        --mount src=ebs-vol, target=/var/lib/mysql mysql `

## Container Storage Interface(CSI):
CRI is a standard that defines how an orchestration tools like Kubernetes would communicate with Container runtimes like Docker.

Similarly CSI was developed to support multiple storage solutions that allows any container orchestration tool to work with storage vendor with a supported plugin.

## Volumes:
In Kubernetes, when a pod is created to process data and then deleted, the data processed by it gets deleted as well. So we will attach a volume to the Pod.

```
apiVersion: v1
kind: Pod
metadata:
    name: volume-sample
spec:
    containers:
    - image: sample-image
      volumeMounts:
      - mountPath: /opt            //Once vol is created, to access it from container, we mount the vol to a dir inside the container.
        name: data-vol
    volumes:
    - name: data-vol
 //Any file created by this pod will be created as a volume and would be stored in the directory data on my node.
      hostPath:
        path: /data
        type: Directory
```
    
