# Running PHP in your very first Docker container

Ever heard of Docker ? This technology is getting very popular in the web development industry, and I've been tinkering with it for a while. What is its purpose and how to take advantage of it? I will take you through the basics now that I'm a little more at ease with it.

<!---more--->

In this tutorial I will make a basic installation PHP inside a container, but I guess you could easily switch it for your favourite language as well. If you've read some posts on this blog, you might have realized how I care about the details (ain't it the title of this blog after all?) ... Though I won't get into the inner workings of Docker, both because it is very obscure to me and because it is more related to system administration while my focus is onto web development. There'll be some Linux command line to type though, but I'll explain each of them, don't worry!
 
## What is a Docker container?

You might wonder why you would change your development environment if it is working for you right now. But you'll eventually want to test a new tool, include some nice dependencies to a some projects, and try your ready to be deployed app in a few different environments just to be sure... All of these reasons might make you change the environment that is shared between all of your projects, so you don't want to mess it up. What if instead, you could use one different environment per project? That's the kind of matter that *Docker* is built for.

Each of such environments will be secluded inside a **container** and each modification in a container won't impact your other containers. That means that every container must include whatever your inside project needs, but not more. You may have been using *virtual machines* for that matter (or maybe not), but containers are not virtual machines. I said I won't expose you the inner mechanics of *Docker*, but be aware that containers are much more **lightweight** than virtual machines. Because contrarily to these, that have to build from the OS every time you create a new one, container are built in layers, that allow them to reuse some already installed components...

One of these layers is the **Linux kernel** from your computer, which is great when you're running a Linux distribution! If you're using *Windows* or *MacOS* don't worry though, because the *Docker* team has published [applications for both these OS](https://docs.docker.com/#run-docker-anywhere) also! I won't guide you through the installation process, because it is already well explained in their documentation, and I've only ever installed it on my *Ubuntu*.

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