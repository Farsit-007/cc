# Docker Bind Mount

## Bind Mount without Volume

```bash
docker run -it --name bind-demo
-v "${PWD}:/app"
-w /app
-p 5000:5000
node:20-alpine sh
-c "npm install -g nodemon && npm install && nodemon --watch /app --legacy-watch index.js"
```

---

## Bind Mount wit Volume

```bash
docker run -it --name bind-demo5
-v "/c/Users/USER/Desktop/Docker/mod-54:/app"
-v node_modules:/app/node_modules
-w /app -p 5000:5000 node:20-alpine sh
-c "npm install -g nodemon && npm install && nodemon --watch /app --legacy-watch index.js"
```

## Inline Env send

```bash
docker run -it --rm -p 5000:5000 -e PORT=5000 -e NODE_ENV=production my-app
```

## Env send from file

```bash
docker run -it --rm --env-file .env -p 5000:5000 my-app
```

## Checking the env on the container

| Command                             | Description                  |
| ----------------------------------- | ---------------------------- |
| `docker exec -it container_name sh` | Enter inside container shell |
| `env`                               | To check any file.           |
| `cat .env`                          | Read the file.               |

Example:

```bash
docker exec -it pet-server sh
```
