## Cache server
Cache server caches sources (only in memory at the moment) for faster access.

## Requirements
- 8 GB ram
- A HTTP2 reverse proxy (nginx, caddy etc)
- A valid SSL certificate (self-signed certs will not work)

## Notes

### SSL
This server does not come with a SSL certificate. Therefore a reverse proxy must be set up to facilitate secure connection to this server. Without a valid SSL certificate, connection to this server will fail as clients only attempt to connect in secure mode.

### Reverse proxy
This server only supports HTTP2, therefore the reverse proxy of choosing must support HTTP2. Discussing reverse proxy configuration is beyond the scope this project. Please pick a reverse proxy you are familiar with.

### Starting the server
To start the server on port `3001`
1. Start `server.exe` from cli

To change the port
1. Create a file `.env` in the same directory with content `PORT=3001`
2. Restart the server.