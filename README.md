# Chirpy

Chirpy is a small social-network-style web server built in Go as part of the Boot.dev backend development course.

The project is built from scratch using Go's standard library and progressively introduces HTTP servers, routing, middleware, JSON APIs, PostgreSQL, SQL queries, authentication, and other backend concepts.

## Features

* HTTP server built with Go
* REST-style API endpoints
* Static file serving
* Health check endpoint
* Request metrics and admin metrics
* JSON request and response handling
* Chirp validation
* Profanity filtering
* PostgreSQL database integration
* SQL migrations with Goose
* User database model

## Technologies

* Go
* `net/http`
* PostgreSQL
* SQL
* Goose
* JSON
* Git

## Project Structure

```text
chirpy/
├── assets/          # Static assets
├── sql/             # Database schema and migrations
├── index.html       # Web page
├── main.go          # Application entry point
├── go.mod           # Go module definition
└── .gitignore       # Git ignore rules
```

## Running the Project

Make sure Go and PostgreSQL are installed and configured.

From the project directory:

```bash
go run .
```

The server runs on:

```text
http://localhost:8080
```

## Learning Project

This repository is primarily a learning project created while working through the Boot.dev backend development curriculum.

The goal is to understand how backend applications work by building the functionality directly rather than relying on a web framework.
