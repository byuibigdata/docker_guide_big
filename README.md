# Docker 

## Introduction

> Docker is to containers as Google is to search

'A container is a special type of process that is isolated from other processes. Containers are assigned resources that no other process can access, and they cannot access any resources not explicitly assigned to them.' The advantages of containers is that a company can create an isolated computer within a computer which provides security and consistency. [raygun.com](https://raygun.com/blog/what-is-docker/#:~:text=In%20conclusion%2C%20Docker%20is%20popular,create%20vast%20economies%20of%20scale.) 

### What are containers?

'Containers sit on top of a physical server and its host OS—for example, Linux or Windows. Each container shares the host OS kernel and, usually, the binaries and libraries, too. Shared components are read-only. Containers are thus exceptionally “light”—they are only megabytes in size and take just seconds to start, versus gigabytes and minutes for a Virtual Machines.'

'Containers also reduce management overhead. Because they share a common operating system, only a single operating system needs care and feeding for bug fixes, patches, and so on. This concept is similar to what we experience with hypervisor hosts: fewer management points but slightly higher fault domain. In short, containers are lighter weight and more portable than VMs.' [blog.netap.com](https://blog.netapp.com/blogs/containers-vs-vms/)

### Why Docker?

'Docker enables developers to easily pack, ship, and run any application as a lightweight, portable, self-sufficient container, which can run virtually anywhere. Containers gives you instant application portability.' 

Containers do this by enabling developers to isolate code into a single container. This makes it easier to modify and update the program. It also lends itself, as Docker points out, for enterprises to break up big development projects among multiple smaller, Agile teams using Jenkins, an open-source CI/CD program, to automate the delivery of new software in containers.[zdnet.com](https://www.zdnet.com/article/what-is-docker-and-why-is-it-so-darn-popular/)

> Docker is to containers as GitHub is to Git

Docker brings several new things to the table that the earlier technologies didn't. The first is it's made containers easier and safer to deploy and use than previous approaches. In addition, because Docker's partnering with the other container powers, including Canonical, Google, Red Hat, and Parallels, on its key open-source component libcontainer, it's brought much-needed standardization to containers.

Since then Docker donated "its software container format and its runtime, as well as the associated specifications," to The Linux Foundation's Open Container Project. Specifically, "Docker has taken the entire contents of the libcontainer project, including nsinit, and all modifications needed to make it run independently of Docker, and donated it to this effort." [zdnet.com](https://www.zdnet.com/article/what-is-docker-and-why-is-it-so-darn-popular/)

### Docker for data science?

Using docker containers means you don't have to deal with "works on my machine" problems. Generally, the main advantage Docker provides is standardization. This means you can define the parameters of your container once, and run it wherever Docker is installed. This in turn provides a few major advantages:

1. __Reproducibility:__ Everyone has the same OS, the same versions of tools etc. This means you don't need to deal with "works on my machine" problems. If it works on your machine, it works on everyone's machine.
2. __Portability:__ This means that moving from local development to a super-computing cluster is easy. Also, if you're working on open source data science projects, like we do at DAGsHub, you can provide collaborators with an easy way to bypass setup hassle.
3. __Docker Hub:__ You can take advantage of the community to find pre-built images [search here](https://hub.docker.com/search?q=data%20science&type=image)

Another huge advantage – learning to use Docker will make you a better engineer, or turn you into a data scientist with super powers. Many systems rely on Docker, and it will help you turn your ML projects into applications and deploy models into production.[dagshub.com](https://dagshub.com/blog/setting-up-data-science-workspace-with-docker/)

## Getting started

1. [Install Docker Descktop](https://www.docker.com/get-started)
2. [Create a Dockerhub account](https://hub.docker.com/signup)
3. [Pull the jupyter/all-spark-notebook](https://hub.docker.com/r/jupyter/all-spark-notebook) `docker pull jupyter/all-spark-notebook`
4. [Create a Docker compose yaml](https://docs.docker.com/compose/)
5. Start your Docker all-spark-notebook container - map to a folder path on your computer `/Users/hathawayj/docker`.

__Command Line__

`docker run --name spark451 -it -p 5000:8888 -p 4040:4040 -p 4041:4041 -v /Users/hathawayj/docker:/home/jovyan/cse451 jupyter/all-spark-notebook`

__Docker Desktop__

<img src="docker_startup.png" width="400" />

6. Now open [http://localhost:5000/lab](http://localhost:5000/lab?token=) and paste `?token=` plus the token shown at the end of the url.

You can find the token in the terminal or in the logs.

| Terminal | Docker Desktop Logs |
|----------|---------------------|
|<img src="terminal_token.png" width="400" /> | <img src="docker_desktop_logs.png" width="400" /> |


[^1]: [raygun.com](https://raygun.com/blog/what-is-docker/#:~:text=In%20conclusion%2C%20Docker%20is%20popular,create%20vast%20economies%20of%20scale.)
[^2]: [blog.netap.com](https://blog.netapp.com/blogs/containers-vs-vms/)
[^3]: [zdnet.com](https://www.zdnet.com/article/what-is-docker-and-why-is-it-so-darn-popular/)
[^4]: [dagshub.com](https://dagshub.com/blog/setting-up-data-science-workspace-with-docker/)
