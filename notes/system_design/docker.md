# Docker
- Tool for running applications in an isolated environment
- **Advantages**:
    - Same environment (Works on all computers if it works on docker)
    - Sandbox Projects (Keeps them separate: no conflicts & better security)
    - Simple to get started on others' projects
- **Containers**: the building blocks of Docker 
    - Stop by themselves when the main process finishes/exits (e.g. php or node.js dies)
    - Should be **one process per container** b/c the life of the container is tied to that process
    - Lightweight so lots of containers can be run on a computer at a time

## Docker vs. Virutal Machines

![Docker v. Vms](https://www.weave.works/assets/images/bltb6200bc085503718/containers-vs-virtual-machines.jpg)

- Docker is less resource heavy than a virtual machine so it is faster than a VM 

## Docker Images

![Docker Image](https://miro.medium.com/max/1273/1*p8k1b2DZTQEW_yf0hYniXw.png)

- A *Dockerfile* is a file with a list of steps to create the image
- A *Docker Image* is a template for creating a desired environment and includes an OS, software, and application code
- A *Docker Container* is a running instance of a docker image



## Setting up a Docker Project

1. Create `Dockerfile` in the root of the project/services directory (outside src folder)
   - Where we will start from an existing image and build on top of it
   - Can find thousands of images on Dockerhub 
2. Write the instructions to build your image in the `Dockerfile`
   - `FROM` specifies the starting/base image to be downloaded from Dockerhub (Must be the 1st line)
   - `COPY` copies the files from the first directory to the second location inside the image (specified in image's documentation)
   - `EXPOSE` tells running containers to listen on the specified port

``` dockerfile
	FROM php:7-0-apache
	COPY src/ /var/www/html
	EXPOSE 80
```

3. Build the docker image from the terminal
   - `-t image-name` specifies the image's name
   - location is the path to the `Dockerfile` which is `.` if in the same directory

```bash
docker build -t image-name location
```

4. Run the docker container from the terminal
   - `-p 80:80` forwards port 80 in the host to port 80 in the container which was exposed in the docker file, allowing it to accept the request so that the code in the container can handle the request

```bash
docker run -p 80:80 image-name
```

## Volumes

- One type allows the sharing of data between containers
- The other type allows the sharing of folders between the host and the container
  - Useful for development since any changes to source code doesn't require a new image to be built and new container to be spun up
  - **Will need to rebuild the image to deploy it** to somewhere else b/c volumes just give the ability for a container to see files on the host's filesystem, **volumes don't change the image**
    - Building an image from a Dockerfile copies the src code so that it can be deployed elsewhere
- Mounting a volume is done when running the container
  - **Must use absolute paths of folders to be mounted** 

```
docker run -p80:80 -v /Users/admin/project/src/:/var/www/html/ image-name
```

## Extra:

```dockerfile
FROM python:3-onbuild
COPY . /usr/src/app
CMD ["python","api.py"]
```

# Docker Compose

- Lets you define all you services/containers in a configuration file 
  - With one command, all the containers can be spun up
- The configuration files save the hassel of writing the docker run commands for each container with all their specifications for volumes and ports
- Creates a virtual network for all the containers allowing communication for all the containers specified in the docker-compose file
  - The host names of the containers match the service names defined in `docker-compose.yml`

## Setting up a Project w/ Docker Compose

1. Create `docker-compose.yml` in root directory of project
2. Write the configuration instructions in docker-compose.yml 
   - Directories are relative to where the docker-compose file is
   - `version` specifies the version of docker-compose file format that you will be writing in (the formats are often updated so this helps specify what syntax you will be using)
   - `build` takes ther relative path to the `Dockerfile` for a container 
   - `volumes` & `ports` allows you to list the volumes and ports for that docker image
   - `depends_on` allows you to specify other services necessary for the service to run

```yml
version: '3'
services:
	product-service:
		build: ./product
		volumes: 
			- ./product:/usr/src/app
		ports:
			- 5001:80
	website:
		image: php:apache
		volumes:
			- ./website:/var/www/html
		ports:
			- 5000:80
		depends_on:
			- product-service
```

3. Spin up the containers running `docker-compose up` from the terminal from the directory where the docker-compose file is located 
   - Will build all the images and then run all the containers
   - Running `docker-compose up -d` will spin up the containers in detached mode meaning you can continue working on the terminal 
     - run `docker ps` to see the status of the containers in detached mode
     - run `docker-compose stop` to stop the containers in detached mode (ctr + c works in nondetached mode)