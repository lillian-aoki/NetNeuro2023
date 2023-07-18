---
title: Programming Power Up 1
layout: main
filename: 01-PP_Containers.md
---
# Containers
<img src=https://www.docker.com/wp-content/uploads/2022/03/horizontal-logo-monochromatic-white.png width=100px>
For scientists containers provide a way of bundling software together to help distribute more reproducible studies in particular it should contain.

* All analysis packages and code
* Operating systems
* It may contain data if it's not too big

Once bundled together this is called an image. i.e. Docker creates a container that runs your image in an isolated place on any machine running docker. 

## Software

There are few ways to create/run containers and images. By far the most popular is a program called [Docker](https://www.docker.com/). Docker is a standard, but it normally requires administrator permissions to install and run. This often limits its use on High-Performance-Computers like Talapas, and alternatives such as [Singularity](https://docs.sylabs.io/guides/3.5/user-guide/introduction.html) are used instead (as a detail Singularity works a bit differently to avoid administrator permissions so things that rely on network connectivity and other base functions may work a bit differently). 

### **Warning** 
Reproducibility isn't the only use for these tools, a lot of the material you'll find online is geared toward organizations running and scaling their code to work for lots of people at once. Reproducibility is helpful in that situation because they need to run the same code in several places and get the same experiences, but they also value easy updating over things like long term archiving. As usual you may find best practices that are conflicting particularly when it comes to efficient updating, and long term reproduciblity.  

# Building a Container

We're going to build and run a docker image. First start out by installing docker

1. Download and install docker desktop following instruction here: https://www.docker.com/

To build a docker image we need a
* **Docker Context** - this is a folder that contains all you code and data you want to package in your image as well as your Dockerfile.
* **Dockerfile** - This is a file that explains to docker how to build your image.

Let's checkout an analysis from git that we want to reproduce
* You'll need to install git if you haven't already please see: (https://github.com/git-guides/install-git)
* We will be running commands in the terminal if you haven't seen this before see here to open a new one: (https://swcarpentry.github.io/shell-novice/)


**2.** To start lets checkout a package that has our docker information in the terminal type

```git clone https://github.com/UO-Data-Science/netneuro-docker.git```

**3.** Now navigate inside that package with
```cd netneuro-docker```

**4.** Let's print out our docker file with
   ```cat Dockerfile```
   
```
FROM rocker/r-ver:latest
WORKDIR /app
COPY . .
RUN apt-get update
RUN apt -y install libcurl4-openssl-dev
RUN R -e "install.packages(c('random'), repos = 'https://cloud.r-project.org/')"
CMD ["Rscript", "code/01-run_me.R"]
```

A Dockerfile is a text file that contains a list of instructions that define your enviroment let's go through this line by line

```FROM rocker/r-ver:latest``` this line selects a base image, this is your starting point and defines your operating system and version you're using. There are several possible base images this one is maintained by The Rocker Project (Docker Containers for the R Environment) https://rocker-project.org/. Base images are a good way to save time, for example this images starts with a linux operating system (Ubuntu) and has everything you need to run base R, so you don't need to include that in your Docker file

```WORKDIR /app``` this tells docker where to put it's file within the container 

```COPY . .``` this tells docker to copy all the files in your current directory (represented by ```.```) into it's working directory also represented by ```.```

The RUN command just tells docker to execute a command on the terminal and in mainly used to install things we'll use it to install the R package 'random'

```RUN apt-get update``` this is needed to install any new packages that are needed on top of the base image

```RUN apt -y install libcurl4-openssl-dev``` an example of installing a new linux package needed by an r-package

```RUN R -e "install.packages(c('random'), repos = 'https://cloud.r-project.org/')"``` this install the R package random

```CMD ["Rscript", "code/01-run_me.R"]``` - finally this is the line that tells docker the command to run when you execute the container, it's the one we've gotten from our git repository.


**5.** To build this image in the same folder (again you'll see your current working directory represented by ```.```) run

```docker build -t my-netneuro-docker .```

Here ```my-netneuro-docker``` is a name you give the new image you've just built, you'll need to remember that for later.

**6.** Finally to run your image type

 ```docker run my-netneuro-docker```

## Questions
* What's your lucky number?
* What's your reproducible number?
* What changes could make this code more inline reproducible standards? 
* Is there a way to make your Lucky Number reproducible?

## Handy Debugging Trick

When you run a docker image it by deaults run's what you tell it too and exits, but this can be annoying if you're trying to fix or debug your docker image. You an also tell docker to run a shell interativly instead of it's default command by typing.

8. ``docker run -i -t my-netneuro-docker bash```

```ctrl+d can be used exit```




