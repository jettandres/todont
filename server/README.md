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

## Choosing a Response Format
The server will feature 2 response formats - JSON and HTML. Use request headers to control the response.

This will be applicable across all endpoints via the `Accept` header.
  - `Accept: application/json` for json response
  - `Accept: text/html` for html response

**JSON API Specification**

JSON format responses will semi-comply with [JSend](https://github.com/omniti-labs/jsend) REST API standard for simplicity.

Semi-comply because the endpoints will not be relying on `.json` but rather more on the request header for format

API Usage
---

### Schema
In compliance with [JSON Schema](https://json-schema.org/learn/getting-started-step-by-step)

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "title": "Todont",
  "description": "A note of not to do",
  "type": "object",
  "properties": {
    "id": {
        "description": "the unique identifier of a todont resource",
        "type": "string"
    },
    "content": {
        "description": "the text body of a todont resource",
        "type": "string"
    }
  },
  "required": ["content", "id"]
}
```


Endpoints
---

### `GET /todonts`
- fetches all todont resource

**response:**
```json
// Accept: application/json
[
  "status": "success",
  "data": {
      "todonts": [
          {
              "id": "84b8075a-bce6-443a-aa48-670615720c3d",
              "content": "feed my cat dog food"
          },
          {
              "id": "10b41abe-db8e-432f-bd01-2cb34652dfa3",
              "content": "bark at my cat"
          }
      ]
  }
]

// TODO: Accept: text/html
```

### `GET /todonts/{id}`
- fetches a specific todont resource

**parameters**
- `id` - the todont id

**response**
```json
// Accept: application/json
{
    "status": "success",
    "data": {
        "todont": {
            "id": "10b41abe-db8e-432f-bd01-2cb34652dfa3",
            "content": "steal my cat's toy"
        }
    }
}

// TODO: Accept: text/html
```

### `POST /todonts`
- inserts a new todont resource

**request**
```json
{
  "content": "rob a bank for ez money"
}
```

**response**
```json
// Accept: application/json
{
  "status": "success",
  "data": {
      "todont": {
          "id": "10b41abe-db8e-432f-bd01-2cb34652dfa3",
          "content": "rob a bank for ez money"
      }
  }
}

// TODO: Accept: text/html
```

### `PATCH /todonts`
- updates a resource with only its specific fields specified.
- used `PATCH` over `PUT` or `POST` for updating since it's not indempotent. [learn more](https://stackoverflow.com/a/34400076)

**request**
```json
{
  "id": "10b41abe-db8e-432f-bd01-2cb34652dfa3",
  "content": "shoot down a helicopter"
}
```

**response**
```json
// Accept: application/json
{
  "status": "success",
  "data": {
      "todont": {
          "id": "10b41abe-db8e-432f-bd01-2cb34652dfa3",
          "content": "shoot down a helicopter"
      }
  }
}

// TODO: Accept: text/html
```

### `DELETE /todonts/{id}`
- deletes a specific resource

**parameters**
- `id` - the todont id

**response**

```json
// Accept: application/json
{
    "status": "success",
    "data": null
}

// TODO: Accept: text/html
```

## Validations and Errors

### Fail
Failed responses are to return `400` status code

when a request has a missing field or incorrect format
```json
// POST /todonts

// request Accept: application/json
{
   "content": null
}

// response
{
   "status": "fail",
   "data": {
       "content": "A content is required"
   }
}

```

when a resource is non existent
```json
// GET /todonts/abc
// DELETE /todont/abc

// response
{
   "status": "fail",
   "data": {
       "id": "Todont resource with id 'abc' does not exist"
   }
}
```

```json
// PATCH /todonts

// request
{
  "id": "abc",
  "content": "take down production"
}

// response
{
    "status": "fail",
    "data": {
        "id": "Todont resource with id 'abc' does not exist"
    }
}

```

### Error
Internal server errors are to return `500` status codes

```json
{
    "status": "error",
    "message": "Unable to connect to database"
}
```
