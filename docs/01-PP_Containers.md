# Containers

For scientists containers provide a way of bundling software together to help distribute more reproducible pipe-lines in particular it should contain

* All Analysis Packages and Code
* Operating Systems
* It may contain data if it's not too big

## Software

There are few ways to create/run containers. By far the most popular is a program called [docker](https://www.docker.com/). Docker is a standard, but it normally requires administrator permissions to install and run. This limitation often limits it use on High-Performance-Computers like Talapas, and alternatives such as [Singularity](https://docs.sylabs.io/guides/3.5/user-guide/introduction.html) are used instead (as a detail Singularity works a bit differently to avoid administrator permissions so things that rely on networks connectivity and other base functions work a bit differently). 

**Warning** reproduciblity isn't the only use for these tools, a lot of the material you'll find online is geared toward organizations running and scaling their code to work for lots of people at once. Reproduciblity is helpful in that situation because they need to run the same code in several places and get the same experience, but they also value easy updating over things like proper archiving. As usually you may find best practices that are conflicting particularly when it comes to efficient updating, and long term reproduciblity.  

# Building a Container

We're going to build and run a docker container.

1. Download and install docker desktop following instruction here: https://www.docker.com/

2. git clone

3. docker build -t my-netneuro-docker .

4. docker run my-netneuro-docker


5. docker run -i -t my-netneuro-docker bash





Containers are normally built from scratch using a configuring file, and any local code you have.


