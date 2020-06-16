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

