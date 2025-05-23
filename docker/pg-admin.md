### Running postgres in docker container
The follwing steps will explain how to run **PostgreSQL** and **PgAdmin** (web) in docker containers.
Using PostgreSQL and PgAdmin in Docker containers offers several benefits:

- **Isolation**: Keeps your database environment separate from your local system, avoiding conflicts.
- **Portability**: Easily share and replicate the setup across different environments.
- **Easy Setup and Maintenance**: Quick to deploy, configure, and manage without affecting your local machine.
- **Cleaner Environment**: No need for local installation, reducing system clutter and making uninstallation easier.
- **Resource Efficiency**: Containers are lightweight and more efficient than full virtual machines.

#### Step-by-step guide:
1. **Install Docker** (if you don't have it installed):
     - Follow the instructions to install Docker: https://docs.docker.com/engine/install/
2. **Run the PostgreSQL Docker container**: Run a PostgreSQL container with a simple docker run command. Open the terminal and run the following:
   ```bash
   docker run --name postgres -e POSTGRES_PASSWORD=password -p 5432:5432 -d postgres
   ```
   - `--name postgres`: Name the container.
   - `-e POSTGRES_PASSWORD=password`: Set the PostgreSQL password.
   - `-p 5432:5432`: Map container’s PostgreSQL port to the host.
   - `-d postgres`: Run the container in detached mode.
3. **Run the PgAdmin container**:
   ```bash
   docker run --name pgadmin -p 5050:80 -e PGADMIN_DEFAULT_EMAIL=admin@admin.com -e PGADMIN_DEFAULT_PASSWORD=admin -d dpage/pgadmin4
   ```
   - `--name pgadmin`: Name the PgAdmin container.
   - `-p 5050:80`: Map PgAdmin’s container port 80 to port 5050 on the host.
   - `-e PGADMIN_DEFAULT_EMAIL=admin@admin.com` Set PgAdmin’s default email.
   - `-e PGADMIN_DEFAULT_PASSWORD=admin`: Set PgAdmin’s default password.
   - `-d dpage/pgadmin4`: Run the PgAdmin container in detached mode.
4. **Verify both services are running**:
   ```bash
   docker ps
   ```
5. **Obtain the IP address of postgres container**:
    ```bash
    docker inspect postgres | grep "IPAddress"
    ```
    This will give the container's IP address, which looks something like this:
   ```bash
   "IPAddress": "172.17.0.2"
   ```
7. **Connect PgAdmin to PostgreSQL**:
   - Access PgAdmin: Open a browser and go to http://localhost:5050. Log in using the credentials that set for PgAdmin (admin@admin.com and admin).
   - Add PostgreSQL server in PgAdmin:
     - Click on the `Add New Server` button.
     - In the `General` tab, give the server a name.
     - In the `Connection` tab, fill out the details:
       - `Host name/address: 172.17.0.2` (the host of the PostgreSQL container).
       - `Port: 5432`.
       - `Username: postgres` (default username).
       - `Password: password` (password set for PostgreSQL).
   
