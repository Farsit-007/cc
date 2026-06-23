## Backend
## Dockerfile

| Command                                                                                                                                                                                                | Description              |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------ |
| `FROM node:22-alpine`<br><br>`WORKDIR /app`<br><br>`COPY package*.json ./`<br><br>`RUN npm ci`<br><br>`COPY . .`<br><br>`EXPOSE 5000`<br><br>`CMD ["sh", "-lc", "npx prisma generate && npm run dev"]` | Backend Dockerfile setup |


## Environment Variable

| Command                                                                                     | Description                        |
| ------------------------------------------------------------------------------------------- | ---------------------------------- |
| `DATABASE_URL=postgresql://postgres:postgres@pet-db-container:5432/ph_server?schema=public` | PostgreSQL database connection URL |

## Docker Network & Volume Setup

| Command                                    | Description                       |
| ------------------------------------------ | --------------------------------- |
| `docker network create pet-network`        | Create Docker network             |
| `docker network inspect pet-network`       | Check network details             |
| `docker volume create client-node-modules` | Create client node_modules volume |
| `docker volume create server-node-modules` | Create server node_modules volume |
| `docker volume create pet-pg-data`         | Create PostgreSQL data volume     |


## Run PostgreSQL Container

| Command                                                                                                                                                                            | Description                                      |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------ |
| `docker run --name pet-db-container --network pet-network -e POSTGRES_HOST_AUTH_METHOD=trust -e POSTGRES_DB=pet_server -v pet-pg-data:/var/lib/postgresql/data postgres:16-alpine` | Run PostgreSQL container with volume and network |

## Build Backend Image
| Command                            | Description                |
| ---------------------------------- | -------------------------- |
| `docker build -t pet-server-dev .` | Build backend Docker image |

## Run Backend Container (Development)
| Command                                                                                                                                                                                                                                                                                                                            | Description                                                            |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| `MSYS_NO_PATHCONV=1 docker run -d --name pet-server --network pet-network --env-file .env -e CHOKIDAR_USEPOLLING=1 -e CHOKIDAR_INTERVAL=300 -p 5000:5000 -v "${PWD}:/app" -v server-node-modules:/app/node_modules -w /app pet-server-dev sh -lc "npm install && npx prisma generate && npx prisma migrate deploy && npm run dev"` | Run backend container with bind mount, volume, env file and hot reload |


## Access Database Container
| Command                               | Description                      |
| ------------------------------------- | -------------------------------- |
| `docker exec -it pet-db-container sh` | Enter PostgreSQL container shell |
| `psql -U postgres -d ph_server`       | Connect to PostgreSQL database   |
| `\dt`                                 | Show database tables             |

## Prisma Migration
| Command                                                         | Description                                             |
| --------------------------------------------------------------- | ------------------------------------------------------- |
| `docker exec -it pet-server sh -lc "npx prisma migrate deploy"` | Run existing Prisma migrations inside backend container |
