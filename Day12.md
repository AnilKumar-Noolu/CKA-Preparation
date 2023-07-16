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
