## Day 17 - Install and Configure PostgreSQL

## Task Details:
The Nautilus application development team has shared that they are planning to deploy one newly developed application on Nautilus infra in Stratos DC. 
The application uses PostgreSQL database, so as a pre-requisite we need to set up PostgreSQL database server as per requirements shared below:

  > PostgreSQL database server is already installed on the Nautilus database server.


a. Create a database user kodekloud_top and set its password to TmPcZjtRQx.


b. Create a database kodekloud_db4 and grant full permissions to user kodekloud_top on this database.


Note: Please do not try to restart PostgreSQL server service.

## Steps:

1. Log in to the Database Server
    ```
    ssh peter@stdb01
    ```

2. Switch to postgres user
    ```
    sudo su - postgres
    ```

3. Access PostgreSQL shell
    ```
    psql
    ```

4. Create the database user
    ```
    CREATE USER kodekloud_top WITH PASSWORD 'TmPcZjtRQx';
    ```

5. Create the database
    ```
    CREATE DATABASE kodekloud_db4;
    ```

6. Grant full privileges on the database
    ```
    GRANT ALL PRIVILEGES ON DATABASE kodekloud_db4 TO kodekloud_top;
    ```

7. Exit PostgreSQL
    ```
    \q
    ```
