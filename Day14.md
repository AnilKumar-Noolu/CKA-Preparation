## Storage
There are mainly 2 concepts of storage in Docker i.e. 1)Storage Driver, 2)Volume Driver
## Storage Driver:
Storage driver help manage storage on images and containers.

By default, Docker stores its file in default folder /var/lib/docker. In Docker, there are 2 types of mounting.
1. Volume Mount: It mounts a volume from the volume directory.
` docker run -v data-vol:/var/lib/mysql mysql`
2. Bind Mount: It mounts a directory from any location on the DockerHost.
` docker run -v /data/mysql:/var/lib/mysql mysql`
