## Run PostgreSQL Container (Local Development)

| Command                                                                                                       | Description                                             |
| ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| `docker run --name pet-db -e POSTGRES_HOST_AUTH_METHOD=trust -e POSTGRES_DB=pet_server -p 5432:5432 postgres` | Run PostgreSQL container with database and port mapping |


## Environment Variable

| Command                                                                      | Description                                                       |
| ---------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| `DATABASE_URL=postgresql://postgres@localhost:5432/pet_server?schema=public` | Connect backend with local PostgreSQL container using mapped port |
