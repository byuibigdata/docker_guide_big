# Docker 

## Introduction

> Docker is to containers as Google is to search

'A container is a special type of process that is isolated from other processes. Containers are assigned resources that no other process can access, and they cannot access any resources not explicitly assigned to them.' The advantages of containers is that a company can create an isolated computer within a computer which provides security and consistency. [raygun.com](https://raygun.com/blog/what-is-docker/#:~:text=In%20conclusion%2C%20Docker%20is%20popular,create%20vast%20economies%20of%20scale.) 

### What are containers?

'Containers sit on top of a physical server and its host OS—for example, Linux or Windows. Each container shares the host OS kernel and, usually, the binaries and libraries, too. Shared components are read-only. Containers are thus exceptionally “light”—they are only megabytes in size and take just seconds to start, versus gigabytes and minutes for a Virtual Machines.'

'Containers also reduce management overhead. Because they share a common operating system, only a single operating system needs care and feeding for bug fixes, patches, and so on. In short, containers are lighter weight and more portable than VMs.' [blog.netap.com](https://blog.netapp.com/blogs/containers-vs-vms/)

### Why Docker?

'Docker enables developers to easily pack, ship, and run any application as a lightweight, portable, self-sufficient container, which can run virtually anywhere. Containers gives you instant application portability.' 

Containers do this by enabling developers to isolate code into a single container. This makes it easier to modify and update the program. It also lends itself, as Docker points out, for enterprises to break up big development projects among multiple smaller, Agile teams using Jenkins, an open-source CI/CD program, to automate the delivery of new software in containers.[zdnet.com](https://www.zdnet.com/article/what-is-docker-and-why-is-it-so-darn-popular/)

> Docker is to containers as GitHub is to Git

Docker brings several new things to the table that the earlier technologies didn't. The first is it's made containers easier and safer to deploy and use than previous approaches. In addition, because Docker's partnering with the other container powers, including Canonical, Google, Red Hat, and Parallels, on its key open-source component libcontainer, it's brought much-needed standardization to containers.

Since then Docker donated "its software container format and its runtime, as well as the associated specifications," to The Linux Foundation's Open Container Project. Specifically, "Docker has taken the entire contents of the libcontainer project, including nsinit, and all modifications needed to make it run independently of Docker, and donated it to this effort." [zdnet.com](https://www.zdnet.com/article/what-is-docker-and-why-is-it-so-darn-popular/)

### Docker for data science?

Using docker containers means you don't have to deal with "works on my machine" problems. Generally, the main advantage Docker provides is standardization. This means you can define the parameters of your container once, and run it wherever Docker is installed. This in turn provides a few major advantages:

1. __Reproducibility:__ Everyone has the same OS, the same versions of tools etc. If it works on your machine, it works on everyone's machine.
2. __Portability:__ This means that moving from local development to a super-computing cluster is easy. Also, if you're working on open source data science projects you can provide collaborators with an easy way to bypass setup hassle.
3. __Docker Hub:__ You can take advantage of the community to find pre-built images [search here](https://hub.docker.com/search?q=data%20science&type=image)

Another huge advantage – learning to use Docker will make you a better engineer, or turn you into a data scientist with super powers. Many systems rely on Docker, and it will help you turn your ML projects into applications and deploy models into production. [dagshub.com](https://dagshub.com/blog/setting-up-data-science-workspace-with-docker/)

## Getting started using `docker run`

1. [Install Docker Descktop](https://www.docker.com/get-started)
2. [Create a Dockerhub account](https://hub.docker.com/signup)
3. [Pull the jupyter/all-spark-notebook](https://hub.docker.com/r/jupyter/all-spark-notebook) `docker pull jupyter/all-spark-notebook`
4. Create a docker network `docker network create n451`
5. Start your Docker all-spark-notebook container - map to a folder path on your computer `/Users/hathawayj/git/BYUI451/docker_guide/data` to a docker volume.

We will see how to [create a Docker compose yaml](https://docs.docker.com/compose/) a little later. _Note that the command line versions require that the full local volume path is specified. We will be able to use relative file paths with the yaml._

__Command Line: Mac__'"

```bash
docker run --name spark -it \
  -p 8888:8888 -p 4040:4040 -p 4041:4041 \
  -v /Users/hathawayj/git/BYUI451/docker_guide/data:/home/jovyan/data \
  -v /Users/hathawayj/git/BYUI451/docker_guide/scripts:/home/jovyan/scripts \
  -v /Users/hathawayj/git/BYUI451/docker_guide/scratch:/home/jovyan/scratch \
  -v /Users/hathawayj/git/BYUI451/docker_guide/work:/home/jovyan/work \
  --network n451 \
  jupyter/all-spark-notebook
```

__Command Line: Windows__

```bash
docker run --name spark -it ^
  -p 8888:8888 -p 4040:4040 -p 4041:4041 ^
  -v C:/git/BYUI451/docker_guide/data:/home/jovyan/data ^
  -v C:/git/BYUI451/docker_guide/scripts:/home/jovyan/scripts ^
  -v C:/git/BYUI451/docker_guide/scratch:/home/jovyan/scratch ^
  -v C:/git/BYUI451/docker_guide/work:/home/jovyan/work ^
  --network n451 ^
  jupyter/all-spark-notebook
```

- [latest java jar for postgres](https://jdbc.postgresql.org/download.html)
- [postgresql-42.2.18.jar in repo](scratch/postgresql-42.2.18.jar)

__Docker Desktop__

<img src="docker_startup.png" width="400" />

6. Now open [http://localhost:8888/lab](http://localhost:8888/lab?token=) and paste `?token=` plus the token shown at the end of the url.

You can find the token in the terminal or in the logs.

| Terminal | Docker Desktop Logs |
|----------|---------------------|
|<img src="terminal_token.png" width="400" /> | <img src="docker_desktop_logs.png" width="400" /> |

### Docker for postgres?

We will use the [PostgreSQL Docker Container](https://hub.docker.com/_/postgres) to create our postgres server and database.  After pulling the container `docker pull postgres` we can get started.

__Command Line: Mac__

```bash
docker run --name db -d -p 5432:5432 \
  -v /Users/hathawayj/git/BYUI451/docker_guide/data/postgresql:/var/lib/postgresql/data \
  -v /Users/hathawayj/git/BYUI451/docker_guide/scratch:/scratch \
  -e POSTGRES_HOST_AUTH_METHOD=trust \
  -e POSTGRES_USERNAME=postgres \
  -e POSTGRES_PASSWORD=postgres1234 \
  --network n451 \
  postgres
```

__Command Line: Windows__

```bash
docker run --name db -d -p 5432:5432 ^
  -v C:/git/BYUI451/Users/hathawayj/git/BYUI451/docker_guide/data/postgresql:/var/lib/postgresql/data ^
  -v C:/git/BYUI451/docker_guide/scratch:/home/jovyan/scratch ^
  -e POSTGRES_HOST_AUTH_METHOD=trust ^
  -e POSTGRES_USERNAME=postgres ^
  -e POSTGRES_PASSWORD=postgres1234 ^
  --network n451 ^
  postgres
```


Now we want to leverage the command line interface within the Docker container.

`docker exec -it db sh`

Once in the docker command line we can interact with our postgres database. We may need to create our database for our 990 tax forms `createdb -U postgres NAMEDB`. For CSE 451, I will share the database files with you. 

We can launch the psql utility to manage the users and database.

`psql -U postgres`

For CSE 450, we want to create a user `USER_NAME` and give them a password `USER_PASSWORD` and connect it to __irs990__ database that I shared.

```bash
create user USER_NAME;
alter role USER_NAME with password 'USER_PASSWORD';
grant all privileges on database irs990 to USER_NAME;
alter database irs990 owner to USER_NAME;
```

Let's create a `webuser` as well becasue our database has that user.

```bash
create user webuser;
alter role webuser with password '2017';
grant all privileges on database irs990 to webuser;
alter database irs990 owner to webuser;
```

#### Restoring a backup file

We can restore the a backup file [ref 1](ttps://docs.bitnami.com/installer/infrastructure/mapp/administration/backup-restore-postgresql/) and [ref 2](https://markheath.net/post/exploring-postgresql-with-docker) but this takes hours for our database.

`psql -U postgres irs990 < /scratch/irsdump_thru_08192020.sql`

- [Meta command psql cheat sheet](https://gist.github.com/Kartones/dd3ff5ec5ea238d4c546)
- [Making my db smaller](https://procrastinatingdev.com/speeding-up-postgres-restores-part-2/)

#### Adminer

Docker Hub has an [adminer image](https://hub.docker.com/_/adminer) that we can pull.

```bash
docker run --name adminer -d -p 8080:8080 --network n451 adminer
```

You can then go to [localhost:8080/](http://localhost:8080/) to see the adminer login. If you haven't created a database, then you can leave `Database` blank.

- System: _PostgreSQL_
- Server: _name of postgres docker_ (db if using the `docker run` command above)
- Username: _postgres_
- Password: _postgres1234_
- Database: _irs990_

## Getting started using `docker-compose`

We can create a docker compose yml that automates a bit of the work we went through above. Once the yml is created, we can simply tell `docker-compose` to build our docker containers. If your terminal is open in the git directory, you can run the following.

`docker-compose -p c451 -f docker-compose.yml up`

One difference is that each docker container will now have new names. 

| docker-compose name     | docker run name     | 
| ----------------------- | ------------------- | 
| _c451_db_1_             | db                  | 
| _c451_spark_1_          | spark               | 
| _c451_adminer_1_        | adminer             | 

With these new names a few commands and inputs will need to be updated.  For example, to get into the new postgres container we would run `docker exec -it c451_db_1 sh`.

[^1]: [raygun.com](https://raygun.com/blog/what-is-docker/#:~:text=In%20conclusion%2C%20Docker%20is%20popular,create%20vast%20economies%20of%20scale.)
[^2]: [blog.netap.com](https://blog.netapp.com/blogs/containers-vs-vms/)
[^3]: [zdnet.com](https://www.zdnet.com/article/what-is-docker-and-why-is-it-so-darn-popular/)
[^4]: [dagshub.com](https://dagshub.com/blog/setting-up-data-science-workspace-with-docker/)
[^5]: https://docs.bitnami.com/installer/infrastructure/mapp/administration/backup-restore-postgresql/ and https://markheath.net/post/exploring-postgresql-with-docker
