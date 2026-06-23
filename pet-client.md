## Frontend
## Dockerfile

| Command                                                                                                                                                                                                                                               | Description               |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------- |
| `FROM node:22-alpine`<br><br>`WORKDIR /app`<br><br>`COPY package.json package-lock.json ./`<br><br>`RUN npm ci`<br><br>`COPY . .`<br><br>`EXPOSE 3000`<br><br>`CMD ["sh", "-lc", "CI=true npm install && npx next dev --webpack -H 0.0.0.0 -p 3000"]` | Frontend Dockerfile setup |


## Environment Variable
| Command                                           | Description                            |
| ------------------------------------------------- | -------------------------------------- |
| `NEXT_PUBLIC_BASE_URL=http://pet-server:5000/api` | Backend API URL for frontend container |

## Build Frontend Image
| Command                            | Description                 |
| ---------------------------------- | --------------------------- |
| `docker build -t pet-client-dev .` | Build frontend Docker image |


## Run Frontend Container (Development)
| Command                                                                                                                                                                                                                                                                                                                                      | Description                                                             |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| `MSYS_NO_PATHCONV=1 docker run -d --name pet-client --network pet-network --env-file .env -e CHOKIDAR_USEPOLLING=1 -e CHOKIDAR_INTERVAL=300 -e WATCHPACK_POLLING=true -p 3000:3000 -v "$PWD:/app" -v client-node-modules:/app/node_modules -w /app pet-client-dev sh -lc "CI=true npm install && npx next dev --webpack -H 0.0.0.0 -p 3000"` | Run frontend container with bind mount, volume, env file and hot reload |


## DB Security

## Run PostgreSQL Container with Password

| Command                                                                                                                                                                                                 | Description                                                                  |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| `docker run --name pet-db-container --network pet-network -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=postgres -e POSTGRES_DB=pet_server -v pet-pg-data:/var/lib/postgresql/data postgres:16-alpine` | Run PostgreSQL container with user, password, database and persistent volume |
