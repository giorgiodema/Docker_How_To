# Docker How to

## Start/Stop Docker
To start, stop docker or to see its status:
```
$ sudo service docker [start|stop|status]
```

## Pull a Docker Image
To pull a docker image from a registry:
```
$ sudo docker pull [OPTIONS] NAME[:TAG|@DIGEST]
```

## Manage Images/Containers
To list the existing images or containers:
```
$ sudo docker [image|container] ls -a
```

To delete all existing containers:
```
$ sudo docker container rm -f $(docker container ls -a -q)
```

## Create/Start Containers
To create and run a docker container from an image:
```
$ sudo docker run [OPTIONS] IMAGE_NAME [COMMAND] [ARG]
```
where useful options are:
- `-v host-src:container-dest` to mount host directories in the running container
- `-it` to run the container interactively
and useful commands are:
- `bin/bash` to spawn a terminal on the running container

## Manage Containers
To execute a command in a running container:
```
$ sudo docker exec [OPTIONS] [CONTAINER_NAME] [COMMAND]
```
In particular to spawn a terminal on an existing container:
```
$ sudo docker exec -it  [CONTAINER_NAME] /bin/bash
```

To save the changes done in a running container, you need the id of the running container (can find it using `sudo docker ps -a`). Then you can save the changes into a 
new image with
```
$ sudo docker commit [CONTAINER_ID] [NEW_IMAGE_NAME]
```

To start, stop a docker container:
```
$ sudo docker [start|stop] [CONTAINER_NAME]
```

## Dockerfile
To create a docker container with a Dockerfile.Run use 
```
$ sudo docker build [PATH]
```
where `[PATH]` is the path of the directory with the dockerfile.
Some useful options that can be specified inside the dockerfile are:
- `FROM [IMAGE_NAME]`, specifies the image from which you are building
- `VOLUME`, creates a mount point in the host filesystem

## Enable Nvidia GPU
To enable nvidia GPU on a docker container you need to install nvidia-docker,
follow the instructions here <a>https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html</a>.
Once nvidia-docker is installed you can run a container with all the GPUs enabled 
running:
```
$ sudo docker run --gpus all [IMAGE_NAME]
```

