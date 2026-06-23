----------------------------
         Backend
----------------------------

```bash
FROM node:22-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .
EXPOSE 5000
CMD ["sh", "-lc", "npx prisma generate && npm run dev"]
```
```bash
DATABASE_URL=postgresql://postgres:postgres@pet-db-container:5432/ph_server?schema=public
```
```bash
1. docker network create pet-network
2. docker network inspect pet-network
3.
     -- docker volume create client-node-modules
     -- docker volume create server-node-modules
     -- docker volume create pet-pg-data
```

```bash
4.docker run --name pet-db-container --network pet-network -e POSTGRES_HOST_AUTH_METHOD=trust -e POSTGRES_DB=pet_server -v pet-pg-data:/var/lib/postgresql/data postgres:16-alpine
```

```bash
5.docker build -t pet-server-dev .
6.MSYS_NO_PATHCONV=1 docker run -d --name pet-server --network pet-network --env-file .env -e CHOKIDAR_USEPOLLING=1 -e CHOKIDAR_INTERVAL=300 -p 5000:5000 -v "${PWD}:/app" -v server-node-modules:/app/node_modules -w /app pet-server-dev sh -lc "npm install && npx prisma generate && npx prisma migrate deploy && npm run dev"
```

```bash
7. docker exec -it pet-db-container sh
8. psql -U postgres -d ph_server
9. \dt
```

```bash
10. --- Existing Prisma migration
docker exec -it pet-server sh -lc "npx prisma migrate deploy"
```