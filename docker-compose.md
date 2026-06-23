services:
```bash
  pet-db:
    image: postgres:16-alpine
    container_name: pet-db-container
    networks:
      - pet-network
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=12345
      - POSTGRES_DB=pet_server
    volumes:
      - pet-pg-data:/var/lib/postgresql/data
    restart: always
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U postgres -d pet_server"]
      interval: 10s
      timeout: 5s
      retries: 5
      start_period: 10s
```
```bash
  pet-server:
    container_name: pet-server
    build:
      context: ./pet-server
      dockerfile: Dockerfile
    restart: unless-stopped
    depends_on:
      pet-db:
        condition: service_healthy
    networks:
      - pet-network
    env_file:
      - ./pet-server/.env
    environment:
      CHOKIDAR_USEPULLING: "1"
      CHOKIDAR_INTERVAL: "300"
    ports:
      - "5000:5000"
    working_dir: /app
    volumes:
      - ./pet-server:/app
      - server-node-modules:/app/node_modules
    command: sh -lc "CI=true npm install && npx prisma generate && npx prisma migrate deploy && npm run dev"
```

```bash
  pet-client:
    container_name: pet-client
    build: 
      context: ./pet-client
      dockerfile: Dockerfile
    restart: unless-stopped
    depends_on:
      pet-server:
        condition: service_started
    networks:
      - pet-network
    env_file:
      - ./pet-client/.env
    environment:
      CHOKIDAR_USEPULLING: "1"
      CHOKIDAR_INTERVAL: "300"
      WATCHPACK_POLLING: "true"
    ports:
      - "3000:3000"
    volumes:
      - ./pet-client:/app
      - client-node-modules:/app/node_modules
    working_dir: /app
    command: sh -lc "CI=true npm install && npx next dev --webpack -H 0.0.0.0 -p 3000"
```

```bash
networks:
  pet-network:
    driver: bridge
```

```bash
volumes:
  pet-pg-data:
  server-node-modules:
  client-node-modules:
```