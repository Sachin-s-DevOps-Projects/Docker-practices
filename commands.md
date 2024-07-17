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
````
docker run -d --name <container  name> <_docker image>
````
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

### 12) Log into a container and access a shell to perform manual operations

````
docker exec -it <container_name> -- /bin/bash
````
````
docker exec -it <container_name> /bin/bash
````
>NOTE- After log into a container, you can use "ctrl + D" keys or "exit" command to exit from the container


### 13) Execute one-off administrative commands or scripts inside a running container without logging into it

````
docker exec <container_name> ls /var/log
````

````
docker exec <container_name> cat /etc/nginx/nginx.conf
````
### 14) We can use monitoring and debugging tools to gather performance metrics or debug running applications
````
docker exec -it <container_name> top
````
### 15)Manage Docker networks such as creating and removing networks, and connecting containers to networks

````
docker network
````
# Docker Volumes

### 16) Lists docker volumes on the host machine
```
docker volume ls
```

### 17) Create a docker volume on the host machine
```
docker volume create <-volume_name->
```

### 18) Get more details about a specific volume
```
docker volume inspect <-volume_name->
```

### 19) Delete a volume
```
docker volume rm <-volume_name->
```

### 20) Using a Volume with a Container (Mount a volume when creating the container )
```
docker run -d --name my-nginx-app --mount source=<-volume_name->,target=/app <-image_name->
             or
docker run -d --name my-nginx-app -v  my-first-volume:/app <-image_name->
```

>Make sure to not make any spaces between sorce and target

>ex: docker run -d --mount source=my-first-volume,target=/app bf3dc08bfed0

*if you haven't created a docker image it , then you can write a image name, then it will pull it from docker hub

```
docker run -d --name my-nginx-app --mount source=<-volume_name->,target=/app nginx:latest
                                    or
docker run -d --name my-nginx-app -v  my-first-volume:/app nginx:latest
```

*This mount will be in a specific directory in Host OS. We dont need it creat it.
Docker will create a logical volume (Tha's mean docker will create a directory) 
in the Host operating system(OS) by itself.

*And the mount will be in /app directory in the container (Because  target=/app )



### 21) Get all details(Inspect) about a specific container including mount details

```
docker inspect <-container_name->
```

Destinations - This will depicts where the mount in container
ex: "Source": "/var/lib/docker/volumes/my-first-volume/_data",

Source       - This will depicts where the mount in host OS
ex:  "Destination": "/app",


### 22)Stops a mount 

>Before stopping a mount, first you must stop the container which has been mounted
>after then container must be removed. Then you'll be able to stop the mount 
````
docker volume <-volume_name->
````

# Docker Networking

### 23) List out all the network on the host machine

````
docker network ls
````

### 24) Remove a docker network

````
docker network rm <network_name>
````

### 25) To create a custome bridge network

````
docker network create <custom_bridge_network_name>
````

### 26) Assign a custom network to a container

Custom Network should be passed while container is creating

````
docker run -d --name <container_name> --network=<custome_breidge> <docker_image>
````
>NOTE: This custom network is completely isolated from other default bride networks. So this container won't be able to comminicate with other containers which has default bridge network

### 27) How to install 'ping' inside a specific docker container
#### You can use the ping command to check if a container is reachable from another container. 
Access the Container:
````
docker exec -it frontend /bin/bash
````
Update the Package List (optional but recommended):
````
apt-get update
````
Install ping (iputils-ping):
````
apt-get install -y iputils-ping
````
Execute Command to test Network Connectivity:
````
ping 172.17.0.3
````
