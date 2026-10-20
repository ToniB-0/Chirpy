# Chirpy

Chirpy is a small social-network-style web server built in Go as part of the Boot.dev backend development course.

The project is built from scratch using Go's standard library, without a web framework. It progressively introduces HTTP servers, routing, middleware, JSON APIs, PostgreSQL, SQL queries, authentication, and other backend development concepts.

## Features

* HTTP server built with Go's standard library
* REST-style API endpoints
* Static file serving
* Health check endpoint
* Request metrics and administrative metrics
* JSON request and response handling
* Chirp creation, retrieval, validation, filtering, and sorting
* Profanity filtering
* PostgreSQL database integration
* SQL migrations with Goose
* Type-safe database queries generated with SQLC
* User registration, login, and account updates
* Password hashing with Argon2id
* JWT access-token authentication
* Refresh tokens and token revocation
* Authorization for protected endpoints and chirp deletion
* Chirpy Red membership upgrades through authenticated webhooks

## Technologies

* Go
* `net/http`
* PostgreSQL
* SQL
* SQLC
* Goose
* JSON
* JWT
* Argon2id
* Git

## Project Structure

```text
chirpy/
├── assets/              # Static assets
├── internal/
│   ├── auth/            # Authentication and security helpers
│   └── database/        # SQLC-generated database code
├── sql/
│   ├── queries/         # SQL queries
│   └── schema/          # Database schema and migrations
├── index.html           # Web page
├── main.go              # Application entry point
├── sqlc.yaml            # SQLC configuration
├── go.mod               # Go module definition
├── go.sum               # Dependency checksums
├── .env                 # Local environment configuration (not committed)
└── .gitignore            # Git ignore rules
```

## Requirements

Before running the project, install and configure:

* [Go](https://go.dev/dl/)
* [PostgreSQL](https://www.postgresql.org/download/)
* [Goose](https://github.com/pressly/goose) for database migrations
* [SQLC](https://sqlc.dev/) for generating database code
* Git

## Installation and Configuration

### 1. Clone the repository

```bash
git clone https://github.com/ToniB-0/Chirpy.git
cd Chirpy
```

### 2. Configure PostgreSQL

Make sure PostgreSQL is running and create a database named `chirpy`.

Configure the database connection using your PostgreSQL username and local database settings.

### 3. Configure environment variables

Create a `.env` file in the project root:

```env
DB_URL="postgres://YOUR_DB_USER@localhost:5432/chirpy?sslmode=disable"
PLATFORM="dev"
TOKEN_SECRET="your-long-random-secret"
POLKA_KEY="your-polka-api-key"
```

Replace the example values with your own configuration. Keep `.env` private and never commit secrets to Git.

### 4. Run database migrations

From the project root, run Goose against your configured database:

```bash
goose -dir sql/schema postgres "YOUR_DATABASE_URL" up
```

Replace `YOUR_DATABASE_URL` with your actual PostgreSQL connection URL.

### 5. Generate database code

Run SQLC from the project root:

```bash
sqlc generate
```

### 6. Install dependencies and start the server

```bash
go mod tidy
go run .
```

The server runs at:

http://localhost:8080

## API Endpoints

| Method   | Endpoint                | Description                             |
| -------- | ----------------------- | --------------------------------------- |
| `GET`    | `/api/healthz`          | Check server health                     |
| `POST`   | `/api/users`            | Register a user                         |
| `PUT`    | `/api/users`            | Update the authenticated user's account |
| `POST`   | `/api/login`            | Log in                                  |
| `POST`   | `/api/refresh`          | Refresh an access token                 |
| `POST`   | `/api/revoke`           | Revoke a refresh token                  |
| `POST`   | `/api/chirps`           | Create a chirp                          |
| `GET`    | `/api/chirps`           | Retrieve chirps                         |
| `GET`    | `/api/chirps/{chirpID}` | Retrieve a specific chirp               |
| `DELETE` | `/api/chirps/{chirpID}` | Delete your own chirp                   |
| `POST`   | `/api/polka/webhooks`   | Process membership upgrade webhooks     |
| `GET`    | `/admin/metrics`        | View fileserver metrics                 |
| `POST`   | `/admin/reset`          | Reset development metrics               |

### Filtering and sorting chirps

The chirp listing endpoint supports optional query parameters.

```bash
# Retrieve all chirps
curl "http://localhost:8080/api/chirps"

# Sort oldest first
curl "http://localhost:8080/api/chirps?sort=asc"

# Sort newest first
curl "http://localhost:8080/api/chirps?sort=desc"

# Retrieve chirps by author
curl "http://localhost:8080/api/chirps?author_id=YOUR_USER_UUID"
```

Replace `YOUR_USER_UUID` with a real user's UUID.

### Authentication

Protected endpoints use bearer access tokens returned by the login endpoint.

```bash
curl -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  http://localhost:8080/api/chirps
```

## Running Tests

Run the Go tests:

```bash
go test ./...
```

Build the project:

```bash
go build
```

For Boot.dev course-specific checks, run:

```bash
bootdev run
```

## Learning Project

Chirpy is primarily a learning project created while working through the Boot.dev backend development curriculum.

The goal is to understand how backend applications work by building the functionality directly rather than relying on a web framework. The project covers practical concepts such as HTTP routing, database persistence, authentication, authorization, and secure API design, providing a foundation for building more advanced backend services.
