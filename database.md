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

[command_line_container.md](command_line_container.md) provides some guidance on getting into the docker command line and using psql within the postgres container.

## Getting started using `docker-compose`

To use this section, I am assuming the following.

- You have cloned this repo to your local computer.
- You have a terminal open at the file path of this cloned repo.
- You have reviewed the [database.md](database.md) guide on the postgress and Adminer containers.
- You have examined the [docker-compose.yml](docker-compose.yml) file.

We can create a docker compose `.yml` that automates a bit of the work we went through above. Once the `.yml` is created, we can simply tell `docker-compose` to build our docker containers. Here are the steps

1. Clone this repository to your computer.
2. Open your terminal and navigate to your git repo directory you just cloned. (Mac: `pwd`, Windows:`cd` to see your working directory)
3. If your terminal is open in the git directory, you can run the `docker-compose`.  The full command - `docker-compose -p c451 -f docker-compose.yml up`.

One difference is that each docker container will now have new names. 

| docker-compose name     | docker run name     | 
| ----------------------- | ------------------- | 
| _c451_db_1_             | db                  | 
| _c451_spark_1_          | spark               | 
| _c451_adminer_1_        | adminer             | 

With these new names a few commands and inputs will need to be updated.  For example, to get into the new postgres container we would run `docker exec -it c451_db_1 sh`.

