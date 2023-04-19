# Docker Cheat Sheet 

This is sample readme file for Docker commands while using NGINX and APACHE

## What is Docker ?
Docker is a popular containerization platform that allows developers to package and distribute applications in lightweight, portable containers. 

## Why Docker ?
These containers provide an isolated environment for running applications and their dependencies, making it easier to deploy applications across different environments. 

## How we are using these concepts here ?
In this context, we are currently using two Docker containers - NGINX and Apache - connected to your web server, which is running on an AWS EC2 instance. We have added two ports, 9091 and 9092, for NGINX and Apache, respectively, and are trying to host your HTML files from your Ubuntu folder on these ports using separate containers. Using two containers in this way can be helpful in achieving better resource utilization and improved availability of our web application, as the load can be distributed between the two containers and they can work together to ensure smooth functioning of your web server. 

## Docker Installation : 
***Connect to your server using following***
```ssh -i ~/.ssh/labsuser.pem ubuntu@yourIPaddress```

***Download and install [Docker Community Edition](https://www.docker.com/pricing/)*** 
If you have Homebrew-Cask, just type ```brew install --cask docker``` 

After installing Docker Community Edition, click the docker icon in Launchpad. Then start up a container using following on your Terminal
```docker run hello-world```

***Version check***
```$ docker --version```

***Use following to add the current user to the Docker group***
The usermod command with -aG option adds the user to the specified group (docker in this case) and $(whoami) is used to get the username of the current user.
```$ sudo usermod -aG docker $(whoami)```

***If you already have Docker, use following to upgrade latest version of Docker***
```$ wget -qO- https://get.docker.com/ | sh```
wget command to download the installation script from the given URL and then pipes the output to the shell (sh) for execution.

## Using Docker Compose: 
##Why Docker Compose?
Without Docker Compose, you would need to manually create and configure networks to connect your containers, and manually set environment variables for each container to point to the other containers. 
Here we using NGINX and Apache hence using Docker compose is a good idea to simplify the start and stop process using single command.


## Docker Compose Installation : 
***Connect to your server using following***
```ssh -i ~/.ssh/labsuser.pem ubuntu@yourIPaddress```

***Install Docker Compose***
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.25.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

***To change the permissions of the Docker Compose binary file to be executable, allowing it to be run as a command.***
```$ sudo chmod +x /usr/local/bin/docker-compose```
```$ sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose```

***Version check***
```$ docker-compose --version```

***Running Docker container: Apache web server to serve the files from the current working directory on the host machine
***
```docker run -dit --name my-apache-app -p 8080:80 -v "$PWD":/usr/local/apache2/htdocs/ httpd:2.4```


Docker commands:

docker start
docker stop
docker ps -a


## Running NGINX using Docker Compose
```$ docker run --name nginx -p 9091:80 -d -v ~/html:/usr/share/nginx/html nginx:1.17```


## Running apache using Docker Compose
```$ docker run --name httpd -p 9092:80 -d -v ~/html:/usr/local/apache2/htdocs/ httpd:2.4```

***Explaining above command***
1. docker run: This option starts a new Docker container based on the provided image.
2. -dit: These are three options provided to the docker run command. The options are:
		* -d: Run the container in the background (detached mode).
		* -i: Keep STDIN open even if not attached.
		* -t: Allocate a pseudo-tty (terminal) for the container.
3. --name my-apache-app: This option provides a name to the container. In this case, the name is my-apache-app.
4. -p 9091:80: This option maps the port 9091 on the host machine to port 80 in the container. 
5. -v ~/html:/usr/share/nginx/html:  This option mounts a volume from the host machine to the container. In this case, the current working directory on the host machine is mounted to the /usr/share/nginx/html directory in the container.
6. httpd:2.4: This is the name of the Docker image that the container will be based on.


## Docker Commands Cheat Sheet : 

| Command | Description |
| -------- | -------- | 
| docker ps | Check running containers|
| docker ps -a | Check all containers|
| docker start dockername| Start container | 
| docker stop dockername| Stop container| 
| docker top id container| Check running processes |
| docker kill $(docker ps -q)| Kill all running containers |
| docker rm -f $(docker ps -qa) | Remove all containers |
| docker rm dockername| Remove specific container |



