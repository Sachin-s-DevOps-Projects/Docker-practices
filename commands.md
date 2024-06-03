# Docker Commands

Some of the most commonly used docker commands are 

### 1) Lists docker images on the host machine
```
docker images
```
To lists latest 5 images,
```
docker images | head -5
```
### 2) Builds image from Dockerfile
````
docker build .
     or
docker buld -t <give_a_name_for_image> .
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

### 9) Login to Docker
````
docker login
````

### 10) Downloads an image from the configured registry
````
docker pull
````




### 11) Uploads an image to the configured registry  

Before this you have to login to docker
````
docker push
````

### 12)Run a command in a running container

````
docker exec
````

### 12)Manage Docker networks such as creating and removing networks, and connecting containers to networks

````
docker network
````

### 13) Lists docker volumes on the host machine
```
docker volume ls
```

### 14) Create a docker volume on the host machine
```
docker volume create <-volume_name->
```

### 15) Get more details about a specific volume
```
docker volume inspect <-volume_name->
```

### 16) Delete a volume
```
docker volume rm <-volume_name->
```

### 17) Using a Volume with a Container (Mount a volume when creating the container )
```
docker run -d --mount source=<-volume_name->, target=/app <-image_name->
```

*if you haven't created a docker image it , then you can write a image name, then it will pull it from docker hub

```
docker run -d --mount source=<-volume_name->, target=/app nginx:latest
```

*This mount will be in a specific directory in Host OS. We dont need it creat it.
Docker will create a logical volume (Tha's mean docker will create a directory) 
in the Host operating system(OS) by itself.

*And the mount will be in /app directory in the container (Because  target=/app )



### 18) Get all details(Inspect) about a specific container including mount details

```
docker inspect <-container_name->
```

Destinations - This will depicts where the mount in container

Source       - This will depicts where the mount in host OS


### 19)Stops a mount 

>Before stopping a mount, first you must stop the container which has been mounted
>after then container must be removed. Then you'll be able to stop the mount 
````
docker volume <-volume_name->
````


