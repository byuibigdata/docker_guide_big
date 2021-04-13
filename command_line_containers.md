# Working in the Docker Container with psql

_This document is currently used for faculty notes._

## Docker command line

Now we want to leverage the command line interface (CLI) within the Docker container.  The command to enter the CLI has four parts.

`docker exec -it db sh` or `docker exec -it db_451 sh`

1. `docker` tells the command line to execute a docker command.
2. `exec` is how you tell Docker to [run a command in a running container](https://docs.docker.com/engine/reference/commandline/exec/).
3. `-it` makes the [container work much like a terminal connection](https://stackoverflow.com/questions/30137135/confused-about-docker-t-option-to-allocate-a-pseudo-tty).
4. `db` the name of the docker container.  We might have `db_451` there as well.
5. `sh` is the command you want to start an shell or terminal connection.

This [docker cli guide](https://www.baeldung.com/linux/shell-alpine-docker) puts a few more words to the above steps.

## psql utility

Once in the docker command line we can interact with our postgresql database. We may need to create our database for our 990 tax forms `create  -U postgres NAMEDB`. _For CSE 451, I will share the database files with you._   

We can launch the psql utility to manage the users and database.

`psql -U postgres`

```bash
create user USER_NAME;
alter role USER_NAME with password 'USER_PASSWORD';
grant all privileges on database irs990 to USER_NAME;
alter database irs990 owner to USER_NAME;
```

### Restoring a backup file

#### Docker 

We can restore the a backup file [ref 1](ttps://docs.bitnami.com/installer/infrastructure/mapp/administration/backup-restore-postgresql/) and [ref 2](https://markheath.net/post/exploring-postgresql-with-docker) but this takes hours for our database.

`psql -U postgres irs990 < /scratch/dump_backup.sql`

#### Azure Database for PostgreSQL server

Assuming you have created the [Azure Database for PostgreSQL](https://azure.microsoft.com/en-us/services/postgresql/) resource and that you are logged into your [portal.azure.com](https://portal.azure.com) account, you can see your `connection strings` by clicking on that named item under `Settings`. Once that window opens, you should see the `psql` string with your appropriate settings.

If you haven't created any databases you can use `dbname=postgres` as shown in the example below.

`psql "host={yourconnection} port=5432 dbname=postgres user={username} password={password} sslmode=require"`

Once connected you can then use any psql functionality.  We want to restore our irs990 data into a database named irs990.  After creating that database with `CREATE DATABASE irs990` you can execute the following restore command (the final element after the `<` should include the file path if you opened your terminal in a directory that doesn't conttain your sql backup).

`psql -h {yourconnection} -p 5432 -U {username} irs990 <  dump_backup.sql`

The [stackoverflow.com response on restorations](https://stackoverflow.com/questions/2732474/restore-a-postgres-backup-file-using-the-command-line).  When you are in `psql` one nice [meta-command](https://gist.github.com/Kartones/dd3ff5ec5ea238d4c546) is `\i` which is the command to execute a shell command.  For example `\i pwd` on Linux or Mac would show your current working directory.

- [Making my db smaller](https://procrastinatingdev.com/speeding-up-postgres-restores-part-2/)
