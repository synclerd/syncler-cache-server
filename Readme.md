## Cache server
Cache server caches sources (in mongodb) for faster access.

## Requirements
- 4+ cores
- 8 GB ram
- A HTTP2 reverse proxy (nginx, caddy etc)
- A valid SSL certificate (self-signed certs will not work)
- A mongodb database

## Notes

### SSL
This server does not come with a SSL certificate. Therefore a reverse proxy must be set up to facilitate secure connection to this server. Without a valid SSL certificate, connection to this server will fail as clients only attempt to connect in secure mode.

### Reverse proxy
This server only supports HTTP2, therefore the reverse proxy of choosing must support HTTP2. Discussing reverse proxy configuration is beyond the scope this project. Please pick a reverse proxy you are familiar with.

### Starting the server
1. Ensure a mongodb database available to use with the application.
2. Download and start the application with following environment variables 
```
PORT=3001
MONGO_CONNECTION_STRING="mongodb://my_user:my_password@my_server_host:my_server_port/"
MONGO_DB_NAME=my_database_name
RESPONSE_LIMIT=1000 #Max number of sources per request
```
3. Run application in maintenance mode by adding the below env variable. Application will exit after completing maintenance. Run this at least once every minute. 
```
MAINTENANCE_MODE=true
```
