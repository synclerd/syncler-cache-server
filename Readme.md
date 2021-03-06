## Cache server
Cache server caches sources (in mongodb) for faster access.

## Requirements
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
1. Make sure you have a mongodb database available to use with the application.
2. Download the application.
3. Create a file in the same directory of the application and name it `.env`
4. Add the following contents.
   Make sure to replace the mongodb connection string and database name with proper values.
```
## Change port
PORT=3001
MONGO_CONNECTION_STRING="mongodb://my_user:my_password@my_server_host:my_server_port/"
MONGO_DB_NAME=my_database_name
```
2. Start `./server` from cli
