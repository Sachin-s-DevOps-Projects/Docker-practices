# Dockerfile Guide

This repository provides a comprehensive guide on how to write Dockerfiles for various types of applications. Dockerfiles are used to automate the creation of Docker images, which are essential for containerizing applications to ensure consistent and reproducible environments.

## Table of Contents

- [What is a Dockerfile?](#what-is-a-dockerfile)
- [Common Dockerfile Instructions](#common-dockerfile-instructions)
  - [FROM](#from)
  - [WORKDIR](#workdir)
  - [COPY](#copy)
  - [ADD](#add)
  - [RUN](#run)
  - [CMD](#cmd)
  - [ENTRYPOINT](#entrypoint)
  - [ENV](#env)
  - [EXPOSE](#expose)
  - [VOLUME](#volume)
  - [USER](#user)
  - [LABEL](#label)
- [Creating a Dockerfile for a Node.js Application](#creating-a-dockerfile-for-a-nodejs-application)
- [Creating a Dockerfile for a Python Application](#creating-a-dockerfile-for-a-python-application)
- [Creating a Dockerfile for a Java Application](#creating-a-dockerfile-for-a-java-application)
- [Best Practices](#best-practices)
- [Building and Running Docker Images](#building-and-running-docker-images)
- [Using .dockerignore](#using-dockerignore)
- [Conclusion](#conclusion)
- [License](#license)

## What is a Dockerfile?

A Dockerfile is a text document that contains all the commands needed to assemble an image. Using `docker build`, users can create an automated build that executes several command-line instructions in succession.

## Common Dockerfile Instructions

### FROM
Sets the base image for subsequent instructions.

#### Examples:
1. Using an official Node.js image:
    ```Dockerfile
    FROM node:14
    ```
    >If you use base image as ubuntu, in this case, there won't be python data.
    >So you have to install it. Otherwise you can select python base image

2. Using an official Ubuntu image:
    ```Dockerfile
    FROM ubuntu:20.04
    ```
    >If you use base image as ubuntu, in this case, there won't be python data.
    >So you have to install it. Otherwise you can select python base image

### WORKDIR
Sets the working directory inside the container. If the directory doesn’t exist, it will be created. It's basically identification on where your source coded is going to save

#### Examples:
1. Setting the working directory to `/app`:
    ```Dockerfile
    WORKDIR /app
    ```

2. Setting the working directory to `/usr/src/app`:
    ```Dockerfile
    WORKDIR /usr/src/app
    ```

### COPY
Copies files or directories from the host machine to the Docker image.

#### Examples:
1. Copying all files from the current directory to `/app` in the container:
    ```Dockerfile
    COPY . /app
    ```

2. Copying only the package.json file:
    ```Dockerfile
    COPY package.json /app/package.json
    ```
>If there is any requirements.txt file, you should first copy that inside your WORKDIR

 ```Dockerfile
    COPY requirements.txt /app
    COPY devops /app
 ``` 

### ADD
Similar to COPY but also supports extracting TAR files and fetching files from URLs.

#### Examples:
1. Adding a file from a URL:
    ```Dockerfile
    ADD https://example.com/file.tar.gz /app/
    ```

2. Extracting a local tar file into the container:
    ```Dockerfile
    ADD app.tar.gz /app
    ```

### RUN
Executes a command in a new layer on top of the current image and commits the results.

#### Examples:
1. Installing a package using apt-get:
    ```Dockerfile
    RUN apt-get update && apt-get install -y curl
    ```

2. Installing Node.js dependencies:
    ```Dockerfile
    RUN npm install
    ```

### CMD
Provides the default command to run when the container starts. This can be overridden at runtime.

#### Examples:
1. Running a Node.js application:
    ```Dockerfile
    CMD ["node", "app.js"]
    ```

2. Running a Python script:
    ```Dockerfile
    CMD ["python", "app.py"]
    ```

### ENTRYPOINT
Configures a container to run as an executable. Unlike CMD, it cannot be overridden easily.

#### Examples:
1. Setting the entrypoint to a script:
    ```Dockerfile
    ENTRYPOINT ["./entrypoint.sh"]
    ```

2. Running a specific command with parameters:
    ```Dockerfile
    ENTRYPOINT ["java", "-jar", "myapp.jar"]
    ```
## What is the difference between ENTRYPOINT and CMD?
```
Basically both ENTRYPOINT and CMD  can be used to execute as your start command. Whenever someone runs docker run both  ENTRYPOINT and CMD  can serve as your starting command. But
But only difference is  ENTRYPOINT something that you can't change. Therfore ENTRYPOINT
should have none overrideable values(We have to put main executables in the ENTRYPOINT ).
Whereas CMD is configurable
If we don't want to let users to change any of things, then we should put it in ENTRYPOINT,
otherwise you can put it in the CMD. 
 
```

### ENV
Sets environment variables.

#### Examples:
1. Setting the NODE_ENV variable:
    ```Dockerfile
    ENV NODE_ENV production
    ```

2. Setting a custom variable:
    ```Dockerfile
    ENV NAME World
    ```

### EXPOSE
Informs Docker that the container listens on the specified network ports at runtime. This does not actually publish the port; it’s for documentation purposes.

#### Examples:
1. Exposing port 3000 for a Node.js application:
    ```Dockerfile
    EXPOSE 3000
    ```

2. Exposing port 80 for a web server:
    ```Dockerfile
    EXPOSE 80
    ```

### VOLUME
Creates a mount point with the specified path and marks it as holding externally mounted volumes from the host or other containers.

#### Examples:
1. Creating a volume at `/data`:
    ```Dockerfile
    VOLUME /data
    ```

2. Creating a volume for a database:
    ```Dockerfile
    VOLUME /var/lib/mysql
    ```

### USER
Sets the user name or UID to use when running the image and for any subsequent RUN, CMD, and ENTRYPOINT instructions.

#### Examples:
1. Switching to a user with UID 1000:
    ```Dockerfile
    USER 1000
    ```

2. Switching to a specific user:
    ```Dockerfile
    USER appuser
    ```

### LABEL
Adds metadata to the image, such as a maintainer’s name or a description.

#### Examples:
1. Adding a maintainer label:
    ```Dockerfile
    LABEL maintainer="name@example.com"
    ```

2. Adding a description label:
    ```Dockerfile
    LABEL description="This is an example image"
    ```

## Creating a Dockerfile for a Node.js Application

### Example Dockerfile

```Dockerfile
# Use an official Node.js runtime as a parent image
FROM node:14

# Set the working directory in the container
WORKDIR /usr/src/app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Make port 3000 available to the world outside this container
EXPOSE 3000

# Define environment variable
ENV NODE_ENV production

# Run the application
CMD ["node", "app.js"]
