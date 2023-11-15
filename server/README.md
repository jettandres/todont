# TODO Server

The app server containing the REST endpoints used to interact with the client

Features:
- Standard library only aside from database drivers for PSQL
- TDD setup from the start
- Supports both JSON and HTML response via the [Accept](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept) request header
  - `Accept: application/json` for json response
  - `Accept: text/html` for html response

## Setup
```bash
# Run test
go test

# Run without docker (db needs to run via docker-compose)
go run .

# Run with docker compose from root
docker compose up server
```
