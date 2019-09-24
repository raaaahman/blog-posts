# Running PHP in your very first Docker container

Ever heard of Docker ? This technology is getting very popular in the web development industry, and I've been tinkering with it for a while. What is its purpose and how to take advantage of it? I will take you through the basics now that I'm a little more at ease with it.

<!---more--->

In this tutorial I will make a basic installation PHP inside a container, but I guess you could easily switch it for your favourite language as well. If you've read some posts on this blog, you might have realized how I care about the details (ain't it the title of this blog after all?) ... Though I won't get into the inner workings of Docker, both because it is very obscure to me and because it is more related to system administration while my focus is onto web development. There'll be some Linux command line to type though, but I'll explain each of them, don't worry!
 
## What is a Docker container?

- secluded
- independant
- ligthweight
- Docker engine operates all the container

## Building an image

- FROM a linux distribution
- RUN some commands
- launch a CMD

## Running the container

- first docker run
- removing the container
- run with another command

## Loading some scripts

- bind mounting at runtime
- WORKDIR and ENTRYPOINT

## Interactive mode

- php interactive shell
- staying alive

## Find images built for you

- from scratch
- DockerHub
- PHP / PHP CLI