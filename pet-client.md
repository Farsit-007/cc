----------------------------
         Frontend
----------------------------

```bash
FROM node:22-alpine

WORKDIR /app

COPY package.json package-lock.json ./

RUN npm ci

COPY . .

EXPOSE 3000

CMD ["sh", "-lc", "CI=true npm install && npx next dev --webpack -H 0.0.0.0 -p 3000"]
```

```bash
NEXT_PUBLIC_BASE_URL=http://pet-server:5000/api
```

```bash
1.docker build -t pet-client-dev .

2. MSYS_NO_PATHCONV=1 docker run -d --name pet-client --network pet-network --env-file .env -e CHOKIDAR_USEPOLLING=1 -e CHOKIDAR_INTERVAL=300 -e WATCHPACK_POLLING=true -p 3000:3000 -v "$PWD:/app" -v client-node-modules:/app/node_modules -w /app pet-client-dev sh -lc "CI=true npm install && npx next dev --webpack -H 0.0.0.0 -p 3000"
```
----------------------------
         DB Security
----------------------------

```bash
docker run --name pet-db-container --network pet-network -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=postgres -e POSTGRES_DB=pet_server -v pet-pg-data:/var/lib/postgresql/data postgres:16-alpine
```