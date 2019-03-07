# Run your projects in Docker containers

It seems that you can't really get around software development without hearing about Docker these days. I won't get into all the reasons why you should care about it, as I'm still pretty new to it myself, but I will share with you the tricks I've found and explain how it help me solve certain problems.

## What are Containers, and why do I use them?

- **process**
- **virtualization**
- **resources**

## Running a container from an existing image.

- **image**
- **Docker Hub**
- **official images**

I will, for example, take the *official image* for Apache Http Server [on this repository](https://hub.docker.com/_/httpd). Its *docker Hub* page indicates that it is the official image, put online by the docker development team; moreover, by visiting the link to [the image's GitHub repository](https://github.com/docker-library/repo-info/tree/master/repos/httpd) I can see that it belongs to the docker-library organization. I, for one, has enough trust in this organization so I will use this image without second though.

- `docker run`

What should I do then with this image? I will create a container from it, by running the following command (which I found in the documentation from the page linked above):

    docker run -dit --name my-apache-app

I believe I should dissect this command to give a more detailed explanation about what it does.

- `docker run` : Tells docker to launch a *new* container, the fact that it's a new one is important, because:
- `--name apache-test` : Assign a name to that particular container. By default, each container is assigned an id which is a long and unique number in hexadecimal notation. As it is helpful to insure there won't be two containers sharing the same id, if you want to retrieve this container to perform further operations on it you will then have to call it by this id, which is not very convenient. Now that I've assigned a *name* to my container, I can access it really easily. But as the command launches a *new* container, this particular name that I chose won't be available to assign to another container, so the `docker run` command will crash if I try to use the same two times in a row. 

## Making your own images

- `docker commit`
- **Dockerfile**

## To be continued
