## Bind Mount without Volume

| Command                                                                                                                                                                              | Description                   |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------- |
| `docker run -it --name bind-demo -v "${PWD}:/app" -w /app -p 5000:5000 node:20-alpine sh -c "npm install -g nodemon && npm install && nodemon --watch /app --legacy-watch index.js"` | Run container with bind mount |

## Bind Mount with Volume

| Command                                                                                                                                                                                                                                              | Description                            |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------- |
| `docker run -it --name bind-demo5 -v "/c/Users/USER/Desktop/Docker/mod-54:/app" -v node_modules:/app/node_modules -w /app -p 5000:5000 node:20-alpine sh -c "npm install -g nodemon && npm install && nodemon --watch /app --legacy-watch index.js"` | Run container with bind mount + volume |

## Inline Env Send

| Command                                                                       | Description                         |
| ----------------------------------------------------------------------------- | ----------------------------------- |
| `docker run -it --rm -p 5000:5000 -e PORT=5000 -e NODE_ENV=production my-app` | Send environment variables directly |

## Env Send from File

| Command                                                   | Description                                 |
| --------------------------------------------------------- | ------------------------------------------- |
| `docker run -it --rm --env-file .env -p 5000:5000 my-app` | Load environment variables from `.env` file |

## Checking Env Inside Container

| Command                             | Description                  |
| ----------------------------------- | ---------------------------- |
| `docker exec -it container_name sh` | Enter inside container shell |
| `env`                               | Check environment variables  |
| `cat .env`                          | Read `.env` file             |
