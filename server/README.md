# TODONT Server

The app server containing the REST endpoints used to interact with the client

Features:
- Standard library only aside from database drivers for PSQL
- TDD setup from the start
- Supports both JSON and HTML response via the [Accept](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept) request header

## Setup
```bash
# Run test
go test

# Run without docker (db needs to run via docker-compose)
go run .

# Run with docker compose from root
docker compose up server
```

## Usage

### Request Headers
Applicable across all endpoints
`Accept`
  - `Accept: application/json` for json response
  - `Accept: text/html` for html response

### `POST /todonts`
- inserts a new todont resource

### `GET /todonts`
- fetches all todont resource

### `GET /todonts/{id}`
- fetches a specific todont resource

### `PATCH /todonts/{id}`
- updates a resource with only its specific fields specified.
- used `PATCH` over `PUT` or `POST` for updating since it's not indempotent. [learn more](https://stackoverflow.com/a/34400076)

### `DELETE /todonts/{id}`
- deletes a specific resource
