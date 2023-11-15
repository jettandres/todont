# TODO App
A fullstack app for learning both FE and BE development

## Todo:
- [ ] Code backend server
- [ ] Code frontend app
- [ ] Setup docker-compose
- [ ] Fill up swagger docs

## Folders

`todo-app`
- folder containing the front-end of the app. I'm planning to use htmx to learn on the go

`todo-server`
- folder containing the server.

`swagger`
- folder containing the swagger documentation. will use this also as practice for documenting my endpoints better

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
