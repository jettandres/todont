# TODONT 🚫
A fullstack app for learning both FE and BE development

## Todo:
- [ ] Code backend server
- [ ] Code frontend app
- [ ] Setup docker-compose
- [ ] Fill up OpenAPI docs
- [ ] Setup e2e with Playwright

## Tech Stack
- App
  - htmx
  - Go
  - PostgreSQL
- CI/CD
  - Github Actions for CI/CD
  - Docker & Docker Compose
- Documentation
  - OpenAPI
  - MermaidJs
- Testing
  - Go standard library (FE/BE)
  - Playwright (E2E)

## File Tree

`app`
- folder containing the front-end components of the app. I'm planning to use htmx to learn on the go

`server`
- folder containing the server.

`docs`
- folder containing the documentation like Swagger/OpenAPI and MermaidJS

`.github`
- contains github actions that perform CI/CD

`docker-compose.yml` file to run the app

## Docker & Docker Compose

Both `app` and `server` will contain their own `Dockerfiles` to run independently

A `docker-compose.yaml` file will be present in root which also initializes a `PostreSQL` database

## Commands
```bash
# start the full app
docker compose up
```
