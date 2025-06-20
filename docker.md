# Docker Commands

## Getting Started

### 1 - Pull Container

```bash
docker pull postgres
```

### 2 - Pull Run Docker With Parameters

Start the Docker container [to run database]. Docker must be running on you computer before this can be done.

```bash
docker run --rm --name postgres --publish 5432:5432 -e POSTGRES_PASSWORD=135791 -v /path/to/local/db/file/on/your/machine:/var/lib/postgresql/data postgres
```

Quick Aside- the above command explained in detail:

docker run //instantiate a container from an image [last parameter]

rm //remove container when done running it

name //name for the container

publish 0000:0000 //the port-mapping docker_engine_port:computer_port

password //sets a password

folder_path/folder_for_local:folder_path/postgres_internal_folder //folder/volume mapping so doesn’t need to start completely from scratch

### 3 - Open zsh For Docker to Execture Commands While Running

In a new terminal window, enter this command to connect to the db container that you just started to run:

```bash
docker exec -it postgres psql -U postgres       //runs a command in a given docker container that is already running
```

### 4 - Execute Commands

```sql
CREATE DATABASE test;

\c test

CREATE TABLE Employees (
 id INT PRIMARY KEY,
 name VARCHAR(35) NOT NULL,
 sal INT );

INSERT INTO Employees VALUES
 (101, 'Sam Mai Tai', 35000),
 (202, 'Morbid Mojito', 65350);
```

### 5 - Verify Database Persistence

Quit database instance:

```bash
 \q
```

Then log back in using steps 1 - 3 and check if your database still has the information you just added by entering this into the szh terminal:

```sql
 SELECT * FROM Employees;
```
