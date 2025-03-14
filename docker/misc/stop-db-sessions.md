### Terminate PostreSQL DB sessions in docker container
Steps to terminate the running **PostgreSQL** DB sessions

1. **Login to the container**: Login to the PostgreSQL container using the below command
   ```bash
   docker exec -it <container-name-or-id> bash
   ```
2. **Login to the PostgresDB**: Login to the database inside the container
   ```bash
   psql -U <database-user> database-name
   ```
3. **Set the schema**: Set the schema of the database.
   ```bash
   set schema <'schema-name'>;
   ```
4. **Terminate the sessions** : Terminate the running sessions using below command
    ```bash
   SELECT pg_terminate_backend(pid)
   FROM pg_stat_activity
   WHERE datname = <'database-name'>
   AND pid <> pg_backend_pid();
   ```
