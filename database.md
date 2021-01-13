## Getting started using `docker run`

In the [README.md](README.md) for this repo you can see an overview of Docker and the steps listed below to get your Spark container working.  This guide will help you get containers for postgress and Adminer running.

1. [Install Docker Desktop](https://www.docker.com/get-started)
2. [Create a Dockerhub account](https://hub.docker.com/signup)
3. [Pull the image](https://hub.docker.com/r/jupyter/all-spark-notebook) `docker pull postgress` and `docker pull adminer`
4. Create a docker network `docker network create n451`
5. Start your Docker containers - map to a folder path on your computer to a docker volume. I have included my path (`/Users/hathawayj/git/BYUI451/docker_guide/data`) which you will need to change. The path to the right of `:` will stay the same.


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

[command_line_container.md](command_line_container.md) provides some guidance on getting into the docker command line and using psql within the postgress container.
