# TODONT 🚫
A fullstack app for learning both FE and BE development

## Todo:
- [ ] Code backend server
- [ ] Code frontend app
- [ ] Setup docker-compose
- [ ] Fill up OpenAPI docs
- [ ] Setup e2e with Playwright

## Tech Stack
- htmx
- Go
- PostgreSQL
- Github Actions for CI/CD

## File Tree

`app`
- folder containing the front-end components of the app. I'm planning to use htmx to learn on the go

`server`
- folder containing the server.

`docs`
- folder containing the documentation like Swagger/OpenAPI and [MermaidJs](https://mermaid.js.org/)

`.github`
- contains github actions that perform CI/CD

## Docker & Docker Compose

Both `todo-app` and `todo-server` will contain their own `Dockerfiles` to run independently

A `docker-compose.yaml` file will be present in root which also initializes a `PostreSQL` database

## Commands
```bash
# start the full app
docker compose up
```
