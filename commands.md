# Docker Commands

Some of the most commonly used docker commands are 

### 1) Lists docker images on the host machine
```
docker images
```

### 2) Builds image from Dockerfile
````
docker build
````

### 3) Runs a Docker container
````
docker run <_docker image>
````
The -it flags tell Docker to make the container interactive and to attach the current shell to the container’s terminal
````
docker run -it <_docker image>
````
You can give a name to your Docker container by using the --name option with the docker run command
````
docker run -it --name <container  name> <_docker image>
````

There are many arguments which you can pass to this command for example,

`docker run -d` -> Run container in background and print container ID
`docker run -p` -> Port mapping

use `docker run --help` to look into more arguments.

### 4)Lists running containers on the host machine

````
docker ps
````
to display container which has been stopped
````
docker ps -a
````

### 5)Stops running container

````
docker stop
````



### 6) Starts a stopped container

````
docker start
````


### 7) Removes a stopped container

````
docker rm <container name>
````
> NOTE - Please make sure to add the container name. It doesn't work for image id or image name

### 8) Removes an image from the host machine
````
docker rmi <image name>
````

### 9) Downloads an image from the configured registry
````
docker pull
````

### 10)Uploads an image to the configured registry

````
docker push
````


### 11)Run a command in a running container

````
docker exec
````

### 12)Manage Docker networks such as creating and removing networks, and connecting containers to networks

````
docker network
````


