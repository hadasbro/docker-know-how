![picture](https://img.shields.io/badge/docker-cheat--sheet-blue)


# 1. General info

Docker Documentation: https://docs.docker.com/

This is just Docker basics tutorial. This wiki includes some basic commands how to use docker containers.

### Table of contents

1. General info 

2. Required programs

3. Installation

	3.1 Windows 

	3.2 Installation on Linux (Ubuntu example)

4. About Docker flow:

	4.1 General flow

	4.2 Container 

	4.3 Image

	4.4 Container examples

5. Commands

	5.1 Basic commands

	5.2 Examples

6. Images and containers

	6.1 Images

	6.2 Containers 

	6.3 Terminal interaction 

	6.4 Useful commands

	6.5 Useful flags

	6.6 Containers states & changes

	6.7 Stopping and removing containers and images

	6.8 Image - Container relation

	6.9 General conslusions

	
7. Working with containers

	7.1 Processes in the container

	7.2 Checking history of operations in the container

8. Files and data volumes

	8.1 "Persistent" data (shared from host or other container)

	8.2 Ephemeral data 

	8.3 Server Http with persistent data

	8.4 Inspect mounts

	8.5 Copying files between container and host

	8.6 Command "docker volume"

9. World of images 

10. Dockerfile	

	10.1 Example of simple Dockerfile:

	10.2 Build an image based on Dockerfile

11. Docker compose

12. Containers networks

13. A - Z example	

* * * 

# 2. Required programs

a) Docker Desktop for Windows (or older Docker Toolbox) https://docs.docker.com/docker-for-windows/

b) Docker CE https://docs.docker.com/install/

c) any SSH client (e.g. Putty) https://www.putty.org/

d) Oracle Virtual Box https://www.virtualbox.org/


* * * 

# 3. Installation

### 3.1 Windows 

a) Install Virtual Box and any SSH client 


b) Install Docker for Windows or Docker Toolbox 


After installation, open Docker Toolbox and run below command to see if it works and to list possible docker commands


```
$ docker
```

> ![docker1.png](https://bitbucket.org/repo/qzxqzMr/images/2972370865-docker1.png)

Also, you can use below command to see more detailed info about docker

```
$ docker info
```

> ![docker2.png](https://bitbucket.org/repo/qzxqzMr/images/1395311743-docker2.png)

Additionally you can try to run hello-world container as below

```
$ docker run hello-world
```

Then you should see some info about pulling hello-world image and status of this operation

> ![docker3.png](https://bitbucket.org/repo/qzxqzMr/images/4112249076-docker3.png)

c) Additional info

Every Toolbox open, should add (if not added yet) and run new box in Oracle Virtual Box (it's because of emulation and ability to run Linux on Windows).

> ![virtual_box_default.png](https://bitbucket.org/repo/qzxqzMr/images/1409310332-virtual_box_default.png)

This Virtual Box, is called "machine", to manage this you can use commands as below:

```
# should show all possible flags and commands

$ docker-machine
```

> ![docker_machine.png](https://bitbucket.org/repo/qzxqzMr/images/3711718026-docker_machine.png)

```
# to log in to the system, inside this virtual box
$ docker-machine ssh
```

> ![docker_machine_ssh.png](https://bitbucket.org/repo/qzxqzMr/images/1972456095-docker_machine_ssh.png)

```
# stop this machine (now on Oracle Virtual Box you should see this machine is stopped)
$ docker-machine stop 

# start this machine
$ docker-machine start 
```

> ![docker_machine_stopper.png](https://bitbucket.org/repo/qzxqzMr/images/1813844174-docker_machine_stopper.png)
> ![docker_machine_stopstart.png](https://bitbucket.org/repo/qzxqzMr/images/1396879387-docker_machine_stopstart.png)

Additionally: in Oracle Virtual Machine you can reserve resources you want to allow for docker machine

_Machine -> Settings -> System_

> ![virtual_machine_settings.png](https://bitbucket.org/repo/qzxqzMr/images/1883400916-virtual_machine_settings.png)

### 3.2 Installation on Linux (Ubuntu example)

a) Installation from repository

How to do: https://docs.docker.com/install/linux/docker-ce/ubuntu/

```
# update packages
$ sudo apt-get update

# install
$ sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common

# install GPG key
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

# verify key 
$ sudo apt-key fingerprint 0EBFCD88

# check if it works
$ sudo docker info

```

> ![docker_info_linux.png](https://bitbucket.org/repo/qzxqzMr/images/2678688772-docker_info_linux.png)

b) Install from package

_@See:_ https://docs.docker.com/install/linux/docker-ce/ubuntu/ (section _Install from a package_)

c) Intall from script		

_@See:_ https://docs.docker.com/install/linux/docker-ce/ubuntu/ (section _Install using the convenience script_)

d) Install in cenOS with SSH client 

```
# install required packages
$ sudo yum install -y yum-utils device-mapper-persistent-data lvm2

# set up repository
$ sudo yum install -y yum-utils device-mapper-persistent-data lvm2

# install docekr CE 
$ sudo yum install docker-ce docker-ce-cli containerd.io

# check
$ docker info
```

> ![docker_info_linux_install.png](https://bitbucket.org/repo/qzxqzMr/images/3886895245-docker_info_linux_install.png)

_@See more:_ https://docs.docker.com/install/linux/docker-ce/centos/ (section _Install using the repository_)




# 4. About Docker flow:

### 4.1 General flow

* _@See_ https://nordicapis.com/api-driven-devops-spotlight-on-docker/

* _@See_ https://medium.com/quick-code/top-tutorials-to-learn-docker-to-run-distributed-applications-bce896e260ec

* _@See_ https://blog.codeship.com/is-docker-secure/

* _@See_ https://medium.com/docker-captain/creating-the-first-docker-image-and-pushing-it-to-docker-hub-4e02bea48e81



### 4.2 Container 

* container is kind of separate machine which is completely independent on master system and also  independent   on other containers.

* container is like a separate world, with it's own system, programs, network etc. 

* container can be moved from one system to another without any changes and it will be working properly as container is just "self contained" object 

* container has his own processes, programs and system (container can have completely different system than the host one)

* container is build based on Image

_Docker is not a Virtual Machine. It doesn't virtualise resources but uses some system's namespaces to create containers, it's kind of fragmentation, there is not resources virtualisation etc.._


_@See more:_ https://www.docker.com/sites/default/files/d8/2018-11/docker-containerized-and-vm-transparent-bg.png

### 4.3 Image

* image is kind of "pattern" for building containers

* images can contain anything, for example complete, installed environment of any kind (e.g. LAMP etc.)

* image can be also a recorded result of any container, the same as we create Containers from Images, we can also create image from Container

### 4.4 Containers example:
_@See_ https://cdn-images-1.medium.com/max/1600/1*Ef2uxCnIkF0PqLGxYqV2gA.png


* * * 


# 5. Commands

### 5.1 Basic commands

```
# to run any command in container use below syntax
$ docker [ TO DO ] [ OPTIONS ] [ IMAGE ] [ COMMAND ] [ PARAMS ]

```

**[ TO DO ]** - what do we want to do, e.g. 

```
# run command
$ run 

# execute command
$ exec

# attach container and process
$ attach
```

**[ OPTIONS ]** - options, e.g. 

```

# terminal
-t 

# interaction
-i

# to set up name of your container
--name name_of_container

# restart
--restart
```

**[ IMAGE ]** - image we want to use as a base for container, e.g.
```
ubuntu:latest
php:7.2-cli
```

see some more images on Docker Hub (https://hub.docker.com)

**[ COMMAND ]** - what to do in container, e.g.:
```
bin/bash
bash
touch super-file.txt
```

**[ PARAMS ]** - additional params 



Docker cheat sheet:

* _@See:_ https://jrebel.com/rebellabs/docker-commands-and-best-practices-cheat-sheet/

* _@See:_ https://www.kdnuggets.com/2018/08/docker-cheat-sheet.html

* _@See:_ https://caylent.com/docker-commands-cheat-sheet/


### 5.2 Examples

```
# create docker container based on nginx image(the latest version), in detached mode (int the background), expose port 80 (map to the same port in host), run nginx server
$ docker run -d -p 80:80 my_image service nginx start


# create docker container based on ubuntu(the latest version), run process /bin/bash inside the container, attach asdin and stdout
$ docker run -a stdin -a stdout -i -t ubuntu /bin/bash


# create docker container with name "my-redis" based on redis image (latest), in detached mode
$ docker run --name my-redis -d redis


# create docker container based on Redis image (latest), run bash process inside, go directly to the container (-ti flag)
$ docker run -it redis bash
```

_@See more:_ https://docs.docker.com/engine/reference/run/

If you run any process in container and if you don't have this container yet and this image in your local repository, 
then Docker will pull needed image and save to your local repository.

* * * 


# 6. Images and containers
### 6.1 Images

```
# to show all images
$ docker images
```

### 6.2 Containers 

```
# show active containers
$ docker ps 

# show all containers (check out statuses)
$ docker ps -a 
```

Why some containers are exited instantly? It's because container works as long as any process inside is running
so if. you run e.g. docker run image - the container will be instantly created and also will finish his work instantly and exit.

Another example of "quick start" and "quick exit"

```
# quickly run container, create file and finish work, so exit container
$ docker run image touch file.txt 
```

How to keep container working?
- run any long - term process in container, e.g. "bash"

```
# run bash in docker container (flag -ti is "terminal interactive" - helps us to go "inside" this container and keep process "bash" active in the container)
# Now container should be "UP" at all time - as long as we keep "bash" inside container working

$ docker run -ti ubuntu bash 
```

How to read docker ps results?

* container id - ID

* image: images used to create container

* command: command ran in the container

* name: name of container (see flags: --name)

* status: just status of container

* created: when created

* ports: ports exposed from container


> ![docker_ps_images.png](https://bitbucket.org/repo/qzxqzMr/images/675455508-docker_ps_images.png)


### 6.3 Terminal interaction 

How to interact with container and go inside the container's system?

```
$ docker run -ti [ container_id_or_image ] [ command ]

# [ container_id_or_image ] - container or image we want to use as a base for container's creation
# [ command ] - command we want to run inside the container
```

example:

```
# container based on image "maven"(lastest)
$ docker run -ti ubuntu:latest /bin/bash


# we can now check if we are really in this container (with Ubuntu, the latest version)
$ cat /etc/lsb-release
```

> ![docker_terminal_interactive.png](https://bitbucket.org/repo/qzxqzMr/images/4259361049-docker_terminal_interactive.png)


### 6.4 Useful commands

Popular Docker commands.

```
# start container (exit directly because there is no keep alive process)
$ docker start -i container_id(e.g. "abc123", see "docker ps -a") 


# almost the same as docker run -ti bash - but it creates new and independent process (run bash inside container and go inside because of -ti - terminal interaction)
$ docker exec -ti container_id(e.g. "abc123", see "docker ps -a") bash 


# go inside the container and connect with currently existing process in the container
$ docker attach container_id(e.g. "abc123", see "docker ps -a") 


# leaving the container and go back to the host
$ exit;


# info about the latest closed container
$ docker ps -l


# inspect image - checking what does image contain?
$ docker inspect [ image ]

$ docker inspect 663c1274dff6 

# log-in and log-out
$ docker logout [SERVER]
$ docker login [OPTIONS] [SERVER]
[OPTIONS]
--password , -p		Password
--password-stdin	Take the password from stdin
--username , -u		Username

```

> ![docker_inspect.png](https://bitbucket.org/repo/qzxqzMr/images/241417730-docker_inspect.png)


```
# inspect container - checking container - on working container we can see some useful info such us network info, IP addresses, exposed ports and more
$ docker inspect [ container ]

$ docker inspect 
```


> ![docker_inspect_container.png](https://bitbucket.org/repo/qzxqzMr/images/550735897-docker_inspect_container.png)


```
# renaming image

$ docker tag image_name new_name:tag
$ docker tag ubuntu my_new_ubuntu:123
```

> ![docker_tag_rename.png](https://bitbucket.org/repo/qzxqzMr/images/2911630813-docker_tag_rename.png)


### 6.5 Useful flags


a) **--name name_of_my_container** - use to force custom name on your container, otherwise random name will be used

```
$ docker run --name my-redis -d redis
```

b) **--restart** - use for managing containers restarts policy. We can use it to keep container alive (even without active process in container). By the default 
this flag is settled as `--restart=no`, that is why if we don't have any alive process in the container, the container is exited just after finish his work.
we can change this behaviour by using this flag, for example:

```
$ docker run -ti --restart unless-stopped --name always_working_container ubuntu bash
```

> ![docker_restart_flag.png](https://bitbucket.org/repo/qzxqzMr/images/404670312-docker_restart_flag.png)

other possible values:

* no [default, restart always when container finish work]
	
* unless-stopped

* on-failure

* always

https://docs.docker.com/engine/reference/run/#restart-policies---restart	

c) **--rm**  - remove image just after finish work (use only for a moment and then remove)

``` 
$ docker run --rm ubuntu echo "something"
```


### 6.6 Containers states & changes
Container automatically saves changes inside. IF we change anything in the container and leave or stop the container, our change will be saved.
Test:

```
# run container and go inside with -ti flag
$ docker run --name my_new_container -ti ubuntu /bin/bash

# create a file inside
$ touch my_new_file.txt

# exit
$ exit;

# go again to container
$ docker start my_new_container
$ docker attach my_new_container
$ ls -la

# we should see our file

```

> ![docker_changes_see1.png](https://bitbucket.org/repo/qzxqzMr/images/745697118-docker_changes_see1.png)
> ![docker_changes_see1.png](https://bitbucket.org/repo/qzxqzMr/images/2926949570-docker_changes_see1.png)


### 6.7 Stopping and removing containers and images

a) Containers

```
# remove container
$ docker rm container_id 
```

in case if container is active (status is "up"), we cannot remove such one, then we have to first stop the container

```
# stop container 
$ docker stop container_id
```

b) Images 	

```
# remove image from local repository
$ docker rmi image_name

# remove image from local repository in case if image is used by any container and cannot be normally removed
$ docker rmi --force
```

c) Bulk operations:

```
# stop all containers we have
$ docker stop $(docker ps -a -q)
 
# delete all containers we have 
$ docker rm $(docker ps -a -q) 

# delete all images
$ docker rmi $(docker images -q) 
```

> ![removeing_containers_and_imgs.png](https://bitbucket.org/repo/qzxqzMr/images/1154668575-removeing_containers_and_imgs.png)


### 6.8 Image - Container relation


Container is always based on image (we need to declare image we want to base, to create any container based on that). 


Also we can create Image based on container. For example if we want to share our work (our container) with someone else, then we can create an Images based on our container and share with someone or just publish e.g. on Docker Hub. 

So, finally if we create a container and then, do some things inside, such us e.g. install some programs etc, then we can finally "export" this container to an Image and share with anyone, so we can share the whole working container.

To do that, we need to commit our container and tag our newly created image

Example:

```
# build a container based on any image
$ docker run --name test_container_and_image_test -ti ubuntu /bin/bash

# add a test file and check
$ touch my_test_file.txt && echo "hehehe" > my_test_file.txt
$ cat my_test_file.txt 
$ ls -la 

```

> ![test_commit1.png](https://bitbucket.org/repo/qzxqzMr/images/3751109476-test_commit1.png)

```
# our newly added file file should be in place, now we can commit our container	
# we can check the last closed container to get his ID
$ docker ps -l


# and commit our container's changes [ docker commit container_ID ]
$ docker commit d79b218d15df 

# commit creates new Image (after commit we should see ID of this image)
# now we should rename this image - set up any better name
```

Syntax:

```
$ docker tag _my_newly_generated_image_name_from_docker_commit my_new_image_name_i_want_to_use
```

Example:

```
$ docker tag 582d90462 my_own_ubuntu_image

# now, we should see our new image (my_own_ubuntu_image) in docker images
docker images
```

Now we can share this image with anyone or load to Docker Hub. Also this image is a complete representation of our container with all his changes inside
so if we create any new container (or anyone else) based on this image - our changes, so e.g. file my_test_file.txt 
will be already added inside

test:

```
# create new container based on our image
$ docker run -ti my_own_ubuntu_image /bin/bash

# list files inside 
$ ls -la 

# as we can see our file is inside (even in new container based on our image)
```

> ![docker_commit_saved.png](https://bitbucket.org/repo/qzxqzMr/images/3572405415-docker_commit_saved.png)

### 6.9 General conslusions

```$ docker run``` ... - creates container based on image


```$ docker commit``` ... - creates a new image, based on container


* * * 



# 7. Working with containers

###Processes in the container

Docker container works like a separate system with all his processes inside. Container's life-cycle strongly depend on main process running on that container.

Test:

```
# create container (in the background)
$ docker run -d -ti --name container_sla1 ubuntu /bin/bash	

# go again into this container on separate window and run bash process again
$ docker run -ti --name container_sla1 ubuntu /bin/bash	

# now we can check if we have 2 separate bin/bash processes
$ ps aux

# now lets kill the main /bin/bash process (PID 1), our container will be exited because we kill main process
```

> ![docker_lifecycle.png](https://bitbucket.org/repo/qzxqzMr/images/2689588822-docker_lifecycle.png)


### 7.2 Checking history of operations in the container

```
$ docker logs [ container_id_or_name ]
$ docker logs container_sla1
```

> ![docker_logs.png](https://bitbucket.org/repo/qzxqzMr/images/30689585-docker_logs.png)

Command ```docker logs``` works on every container, no matter what is the container's state.


* * * 


# 8. Files and data volumes

Data volumes functionality in kind of mapping between local host and container. We can use this to share some HDD space or directory between container and host system.


### 8.1 "Persistent" data (shared from host or other container).

How to share volume - map host directory to docker container's one?

Example (mapping my /home directory to /dir_in_container in the container)

```
$ docker run -ti --name my_container -v "$(PWD)":/dir_in_container ubuntu /bin/bash
```

Now if we add any file or edit anything in host machine, then it will be available in the container as well. Also, if we remove container, then 
data on host will still be there of course.

Mounting  volume give us possibility to create "data - transparent" images & containers, so mounted data will not be saved in container and image but 
will be stored just on host machine. Also mounted data is not committed to an image if we use `docker commit`.

> ![mount_v.png](https://bitbucket.org/repo/qzxqzMr/images/1709790906-mount_v.png)

### 8.2 Ephemeral data 

Ephemeral data is available only inside the container and is removed once we remove container.

Example:

```
# create container and add a test file inside
$ docker run -ti --name container1 -v /my_volume1 ubuntu bash

$ touch ./my_volume1/test_file.txt && echo "some info" >> ./my_volume1/test_file.txt

$ cat ./my_volume1/test_file.txt

# create second container using data volum from the first container
$ docker run -ti --name container2 --volumes-from container1 ubuntu bash

# put some data to this file from container 2
$ cd ./my_volume1/
$ echo "new data from container 2"  >> test_file.txt
$ cat ./test_file.txt

# exit container 1 and remove
$ exit;
$ docker rm [container 1] 

# try to create another container with volume shared with container1
$ docker run -ti --name container5 --volumes-from container1 ubuntu bash

# error
so we lost data from container 1
```


> ![volumesx.png](https://bitbucket.org/repo/qzxqzMr/images/2018847913-volumesx.png)
> ![docker_mountx2.png](https://bitbucket.org/repo/qzxqzMr/images/3040643431-docker_mountx2.png)

### 8.3 Server Http with persistent data

Server Http with persistent data volume (from host).

```
# create directory on host and add index.html file inside
/server_files/index.html (<html><h1>This is my index!!!</h1></html>)

# create docker container based on httpd image and mount host's /server_files directory to container's /htdocs directory (public apache server's directory) + expose port 80 to 8080
$ docker run -dti --name my_server -p 8080:80 -v //c/Users/S/server_files:/usr/local/apache2/htdocs httpd

```

Our host's index.html should be now visible in the container's htdocs directory

Now we can go to host, open the browser and type
localhost:8080
or (default docker machine IP)
http://192.168.99


and we should see our index.html file's contend so our server in on docker container but data (index file) is on host and it's is Persistent data (will not disappear if we remove container).


> ![mount_httpd.png](https://bitbucket.org/repo/qzxqzMr/images/3401764761-mount_httpd.png)


### 8.4 Inspect mounts

```
# use docker inspect command to check mounts
$ docker inspect container 
```

> ![docker_mounts.png](https://bitbucket.org/repo/qzxqzMr/images/1488836082-docker_mounts.png)

### 8.5 Copying files between container and host

**From host to container**

```
$ docker cp FILE_OR_DIR_TO_COPY containerName:/path_in_container
```

Example:

```
$ cd /c/Users/S/
$ docker cp ./server_files/ my_server:/my_files

# now we should see copied directory in the container

```


> ![docker_cp.png](https://bitbucket.org/repo/qzxqzMr/images/851840122-docker_cp.png)

**From container to host**

```
$ docker cp containerName:/path_in_container where_to_copy_in_the_host

$ docker cp my_server:/my_files C:/
```

> ![docker_cp2.png](https://bitbucket.org/repo/qzxqzMr/images/1321903812-docker_cp2.png)

### 8.6 Command "docker volume"


Creating volumes and managing columens.

**Create new volume**

```
$ docker volume create my_new_volumen

# now we can mount this volume to any container

$ docker run -ti --name my_volums --mount source=my_new_volumen,target=/my_mounted_data ubuntu bash

# check if we have directory mounted
$ ls

# now we can add or edit any file in the host and it will be visible in container
```


**Other operations on volumes**

```
# inspecting volume
$ docker volume inspect [ volume_name ]
$ docker volume instect my_new_volumen


# removing volumes
$ docker volume rm [ volume_name ]
$ docker volume rm my_new_volumen

# removing unused volumes
$ docker volume prune my_new_volumen


# bulk remove unused

$ docker volume prune $(docker volume ls -q)
```



**Useful flags**

```
$ docker volume create my_new_volumen --label "My new Label"  # creating custom labels
```

> ![docker_volumes5.png](https://bitbucket.org/repo/qzxqzMr/images/2914581439-docker_volumes5.png)


* * * 




# 9. World of images 

There are a lot of images ready to use in the internet, almost with every possible service and configuration already installed.

#### a) Docker Hub - the world's largest library and community for container images
https://hub.docker.com/

#### b) search images via docker command

Syntax:

```
$ docker search [ image_name_or_part ]
```

Example:

```
$ docker search ubuntu 
```

#### c) pulling images to local repository (without creating container)

Syntax:
```
$ docker pull [ image ]
```

Example:
```
$ docker pull ubuntu
```

> ![docker_search.png](https://bitbucket.org/repo/qzxqzMr/images/1518977206-docker_search.png)

#### d) sending images to public or private repository
We need to prepare an image, tag this image and then push to any repository.


```
# prepare image with tag and repository 
$ docker tag [ image ] [our_docker_hub_repository]/[ our_image_name ]:[ tag ] 

$ docker tag ubuntu slawekhaa/my_own_ubuntu:1.01

# log in to docker hub
$ docker login
# + authenticate

# push to docker hub
$ docker push slawekhaa/my_own_ubuntu:1.01

# now everybody can use this image and build container based on it
```

> ![docker_push.png](https://bitbucket.org/repo/qzxqzMr/images/1428380660-docker_push.png)
> ![docker_hub.png](https://bitbucket.org/repo/qzxqzMr/images/711645227-docker_hub.png)


* * * 


# 10. Dockerfile	
Dockerfile is kind of script or image's description (set of commands) we can use to build an image.
The order of commands in Dockerfile is important.

#### 10.1 Example of simple Dockerfile:

```
# Comment (e.g. "server with php")

# image we want to use to build an image
FROM ubuntu

# maintainer information
MAINTAINER Slawek <email@example.com>

# analogically we can use (in this case we can see the Label in docker inspection - docker inspect)
# LABEL maintainer="Slawek <email>"

# commands to run in the image after build (here it's PHP installation + packages update)
RUN apt-get update && \ 
apt-get install -y apache2 vim nano php7.0 libapache2-mod-php7.0 php7.0-mysql php7.0-cli && \
apt-get clean && \ 
rm -rf /var/lib/apt/lists/*

# [ optional ] - environment variables we want to set
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2 

# more commands (here we create a phpinfo file)
# better is to write all commands in the single RUN clausule because the Docker will create less 
# amount of containers behind and finally our container's size will be smaller
RUN echo "<?php  phpinfo() ?>" > /var/www/html/phpinfo.php

# optional (if we want to create container for specific user only instead of default user - root)
# after build we can check user's dir > pwd and it should be our newly added user
RUN useradd -ms /bin/bash slawek
USER slawek

# port we want to expose or map from container to the host system
EXPOSE 80

# [ optional ] command we can use at the moment when container id build
# unlike RUN - CMD is used when container is build, while RUN is used when image is build
# in this example we just run apache in the background
CMD apachectl -D FOREGROUND 

```




#### 10.2 Build an image based on Dockerfile

```
# Syntax
$ docker build -t [ image_name_we_want ] [ dockerfile_path ]

# Example
$ cd /dockerfile_path
$ docker build -t serverssh ./
```


> ![dockerfile.png](https://bitbucket.org/repo/qzxqzMr/images/4213435093-dockerfile.png)

After build we can check our image IP and check if our server works e.g.

```
$ docker inspect our_image | grep IPAddress
$ elinks our_container_ip

```


> ![docker_ip_call.png](https://bitbucket.org/repo/qzxqzMr/images/4269093620-docker_ip_call.png)

#### 10.3 Dockerfile cheatsheet
https://miro.medium.com/max/1273/1*p8k1b2DZTQEW_yf0hYniXw.png


* * * 



# 11. Docker compose


Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services. Then, with a single command, you create and start all the services from your configuration. To learn more about all the features of Compose, see the list of features.

Compose works in all environments: production, staging, development, testing, as well as CI workflows. You can learn more about each case in Common Use Cases.

Using Compose is basically a three-step process:

* Define your app’s environment with a Dockerfile so it can be reproduced anywhere.

* Define the services that make up your app in docker-compose.yml so they can be run together in an isolated environment.

* Run docker-compose up and Compose starts and runs your entire app.

Example of Docker compose file:

```
docker-compose.yml

mysql-docker:
container_name: mysql_docker
image: mysql:5.7
environment:
- MYSQL_ROOT_PASSWORD=root
- MYSQL_DATABASE=realtime_notifer
- MYSQL_USER=sla
- MYSQL_PASSWORD=sla

boot-rethink:
container_name: rethinkdb_docker
image: rethinkdb
ports:
- 8080:8080
- 28015:28015
- 29015:29015

realtime-notifer-docker:
container_name: realtime_notifer
image: slawekhaa/realtime_notifer
links:
- mysql-docker:mysql
- boot-rethink:rethink
ports:
- 8090:8090
```



Example of Dockerfile to build custome image realtime_notifer

```
Dockerfile

FROM java:8
ADD realtime_notifer.jar app.jar
RUN bash -c 'touch /app.jar'
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-Dspring.profiles.active=docker","-jar","/app.jar"]
```


How to run

```
$ cd docker-compose.yml

$ docker-compose up
```

Final result: we should have 3 working containers with MySQL, RethikDb database and Java application, linked between each other.



# 12. Containers networks

... section in progress ...

# 13. A - Z example	
a) Server apache + PHP 
Use Dockerfile from this repository - */apache_php/Dockerfile*. Dockerfile contains commands needed to install Apache server with PHP 7.

```
# go to the Dockerfile directory
cd directory_with_dockerfile

# use our Dockerfile to build an image
$ docker build -t apache_php_slawek ./

# build a container + map port 8080 to 80 and mount host's home directory to server's www/html directory
$ docker run -tid --name MyApachePhpServer -p 8080:80 -v "$PWD":/var/www/html ubuntu:apache_php_slawek 

# now we can add a phpinfo.php file and try to reach this server from host e.g. via elinks
# now we should have working Apache server with PHP
elinks http://localhost:8080

```

> ![real_example_php.png](https://bitbucket.org/repo/qzxqzMr/images/3827319137-real_example_php.png)

See official PHP images on Docker Hub https://hub.docker.com/_/php


b) Server SSH

Use Dockerfile from this repository - */ssh_caontainer/Dockerfile*

```
# go to the Dockerfile directory
cd directory_with_dockerfile

# use our Dockerfile to build an image
$ docker build -t serverssh ./

# build a container based on our image
$ docker run -tid serverssh -p 2022:22

# now weshould have working container with SSH


```

> ![example_ssh.png](https://bitbucket.org/repo/qzxqzMr/images/1832044665-example_ssh.png)

* * * * *

The end.

## Authors

* **Slawomir Hadas** - *author* - [Github](https://github.com/hadasbro)
