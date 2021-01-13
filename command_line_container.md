# Working in the Docker Container with psql

## Docker command line

Now we want to leverage the command line interface within the Docker container.

`docker exec -it db sh`

## psql utility

Once in the docker command line we can interact with our postgres database. We may need to create our database for our 990 tax forms `create db -U postgres NAMEDB`. For CSE 451, I will share the database files with you. 

We can launch the psql utility to manage the users and database.

`psql -U postgres`

For CSE 451, we want to create a user `USER_NAME` and give them a password `USER_PASSWORD` and connect it to __irs990__ database that I will share.

```bash
create user USER_NAME;
alter role USER_NAME with password 'USER_PASSWORD';
grant all privileges on database irs990 to USER_NAME;
alter database irs990 owner to USER_NAME;
```

Let's create a `webuser` as well because our database has that user.

```bash
create user webuser;
alter role webuser with password '2017';
grant all privileges on database irs990 to webuser;
alter database irs990 owner to webuser;
```

### Restoring a backup file

We can restore the a backup file [ref 1](ttps://docs.bitnami.com/installer/infrastructure/mapp/administration/backup-restore-postgresql/) and [ref 2](https://markheath.net/post/exploring-postgresql-with-docker) but this takes hours for our database.

`psql -U postgres irs990 < /scratch/irsdump_thru_08192020.sql`

- [Meta command psql cheat sheet](https://gist.github.com/Kartones/dd3ff5ec5ea238d4c546)
- [Making my db smaller](https://procrastinatingdev.com/speeding-up-postgres-restores-part-2/)
