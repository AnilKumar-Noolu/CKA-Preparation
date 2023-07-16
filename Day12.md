## Image Security
Generally in a pod or deployment, we will be using public images available in DockerHub.

To run pods/deployment with private images, then we need to implement full name of iamge in yaml file.

Now the question is Authentication part, How does Kubernetes implement login part to access private registry. As Images are pulled by Docker runtime on Worker Node.

Create a Secret object in Kubernetes with credentials on it and reference that secret object in yaml file.
```
kubectl create secret docker-registry regcred \
        --docker-server=<pvt-registry.io> \
        --docker-username=<username> \
        --docker-password=<password> \
        --docker-email=<email_id>

In pod.yaml file

spec:
  containers:
  - name:
    image: pvt-registry.io/apps/internal
  imagePullSecrets:
  - name: regcred
```

## Security in Docker
We can set USER_ID in Dockerfile or in the docker commands to run that commands as that User.

docker run --user=1001 ubuntu sleep 300

By default, Docker runs a conatiner with a limited set of Capabalities and so the process running within container do not have privileges to say reboot host or Perform operations.

#### commands
docker run --cap-add MAC_ADMIN ubuntu                            // To add new Privilege to the container

docker run --cap-drop MAC_ADMIN ubuntu                           // To drop new Privilege to the container

docker run --privileged ubuntu                                  // To run the container with all privileges

In K8, the settings on container will override settings on Pod. If you apply settings on pod, it will apply to all containers in that Pod.
```
Pod-security:

spec:
  SecurityContext:
     runAsUser: 1001

Container-security:

spec:
  SecurityContext:
    runAsUser: 1001
    capabilities:
        add: ["MAC_ADMIN"]    //To add additional privileges to that existing user/container
```
