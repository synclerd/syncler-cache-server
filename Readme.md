## Cache server
Cache server caches sources for faster access.

## Requirements
- 4+ cores
- 8 GB ram
- A HTTP2 reverse proxy (nginx, caddy etc)
- A valid SSL certificate (self-signed certs will not work)
- Docker compose

## Notes

### SSL
This server does not come with a SSL certificate. Therefore, a reverse proxy must be set up to facilitate secure connection to this server. Without a valid SSL certificate, connection to this server will fail as clients only attempt to connect in secure mode.

### Reverse proxy
This server only supports HTTP2, therefore the reverse proxy of choosing must support HTTP2. Discussing reverse proxy configuration is beyond the scope this project. Please pick a reverse proxy you are familiar with.

### Starting the server
- Create `docker-compose.yml` with the following.
```
services:
  app:
    image: ghcr.io/synclerd/cache-server:<tag> 
    container_name: syncler-cache-server
    restart: unless-stopped
    depends_on:
      - db
    environment:
      MONGO_CONNECTION_STRING: mongodb://db:27017
      MONGO_DB_NAME: cache-server
      RESPONSE_LIMIT: 1000
    ports:
      - 127.0.0.1:3001:3001

  db:
    image: mongo
    restart: unless-stopped
    volumes:
      - syncler-cache-server-data:/data/db
    
volumes:
  - syncler-cache-server-data
```
- Replace `<tag>` in `docker-compose.yml` with the latest tag. Find the latest version @ [https://github.com/synclerd?tab=packages](https://github.com/synclerd?tab=packages)
- Run `docker compose up -d`
- Setup corn (or run manually) for maintenance `docker exec -e MAINTENANCE_MODE=true syncler-cache-server /bin/sh -c '/app/cache-sever'`.
MAINTENANCE_MODE=true
```
