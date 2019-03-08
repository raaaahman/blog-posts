# Run your projects in Docker containers

It seems that you can't really get around software development without hearing about Docker these days. I won't get into all the reasons why you should care about it, as I'm still pretty new to it myself, but I will share with you the tricks I've found and explain how it help me solve certain problems.

## What are Containers, and why do I use them?

- **process**
- **virtualization**
- **resources**

## Creating containers from existing images

- **image**
- **Docker Hub**
- **official images**

I will, for example, take the *official image* for Apache Http Server [on this repository](https://hub.docker.com/_/httpd). Its *docker Hub* page indicates that it is the official image, put online by the docker development team; moreover, by visiting the link to [the image's GitHub repository](https://github.com/docker-library/repo-info/tree/master/repos/httpd) I can see that it belongs to the docker-library organization. I, for one, has enough trust in this organization so I will use this image without second though.

## Running a container

What should I do then with this image? I will create a container from it, by running the following command (which I found in the documentation from the page linked above):

    docker run --name apache-test -dit httpd

I believe I should dissect this command to give a more detailed explanation about what it does.

- `docker run` \*: Tells docker to launch a *new* container, the fact that it's a new one is important, because:
- `--name apache-test` : Assign a name to that particular container. By default, each container is assigned an id which is a long and unique number in hexadecimal notation. As it is helpful to insure there won't be two containers sharing the same id, if you want to retrieve this container to perform further operations on it you will then have to call it by this id, which is not very convenient. Now that I've assigned a *name* to my container, I can access it really easily. But as the command launches a *new* container, this particular name that I chose won't be available to assign to another container, so the `docker run` command will crash if I try to use the same two times in a row.
- `-d` : Will run your container in *detached mode*. This simply means that, contrary to *attached mode*, which is the default mode, it won't automatically log it's activity in your terminal session, making it available to use type more commands in it.
- `-i` : Will run the container in *interactive mode*. Basically, when you run any container, it will execute a **process** and then will stop when this process is terminated. Interactive mode however, will make your container wait for instructions even after it has finished it's process. This means that such a container will be always running, so you will have to shut it down manually. We'll see how to do that a little later.
- `-t` : Will allow to access this container opening distant shell command session, this will give you the possibility to access the linux system running in your container in your host machine's terminal. We will do that in the next chapter.
- `httpd` : Finally, this is the **docker image** from which we are building the container. This image contains the description on the steps docker will need to perform to install the basic components required to run an Apache Http Server, including the OS installation and the Apache Http Server itself (which is still called *httpd* inside some Linux distributions).

## Interacting with a running container

Now that I have my container running, I can easily access it by typing this command:

  docker exec -i -t apache-test /bin/bash

We'll go into it in details:

- ``

_\* : Because Docker access to system components on your computer, you will have to give it root user permissions, that means basically every right. There's different ways to achieve it, and it may depend on your OS (I've never tried Docker for Windows or OsX), but the easiest is to simply prefix each Docker command with `sudo`, which will grant Docker root permissions for this single command._

## Making your own images

- `docker commit`
- **Dockerfile**

## To be continued
