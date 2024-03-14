# PracticalSQL docker-compose project

This project contains Docker Compose configuration for running PostgreSQL and pgAdmin instances to follow along
with the [Practical SQL 2nd Edition](https://nostarch.com/practical-sql-2nd-edition) book.

## Configuration

### Environment Variables

To configure the services, copy the `.env.sample` file to `.env` and set the following variables:

```dotenv
POSTGRES_USER=USERNAME
POSTGRES_PASSWORD=PASSWORD
POSTGRES_DB=DATABASE-NAME
PGADMIN_DEFAULT_EMAIL=LOGIN-EMAIL
PGADMIN_DEFAULT_PASSWORD=LOGIN-PASSWORD
PGADMIN_USER_FOLDER=LOGIN-EMAIL-NO-AT
```

### Datasets

Ensure that datasets are stored in the correct folder:

```plaintext
./datasets:/data
```

Ensure correct permissions for the dataset folder:

```bash
sudo chmod -R 777 /home/USERNAME/practicalsql/datasets
```

## Services

### PostgreSQL

Runs the PostgreSQL database server.

- Image: `postgis/postgis:13-3.4-alpine`
- Volumes:
  - Postgres data: `postgres-data:/var/lib/postgresql/data`
  - Dataset access: `./datasets:/data`

### pgAdmin

Runs the pgAdmin web interface.

- Image: `dpage/pgadmin4`
- Ports: `8080:80`
- Depends on: `postgres`

## Usage

To start the services, run:

```bash
docker-compose up -d
```

To stop the services, run:

```bash
docker-compose down
```
