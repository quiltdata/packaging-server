# POEM OpenAPI v5 TODOs Example

This is a simple example of a TODOs API using the POEM OpenAPI v5 framework.

## Setup

### 1. Declare the database URL

```sh
export DATABASE_URL="sqlite:todos.db"
```

### 2. Create the database

```sh
sqlx db create
```

### 3. Run sql migrations from ./migrations

```sh
sqlx migrate run
```

## Usage


### 1. Start the server

```sh
cargo run &
```

### 2. Open user-facing URLs

```sh
open http://localhost:3000/ui
open http://localhost:3000/spec
```

### 3. POST a todo

```sh
curl -X 'POST' \
  'http://localhost:3000/todos' \
  -H 'accept: application/json; charset=utf-8' \
  -H 'Content-Type: text/plain; charset=utf-8' \
  -d 'This is a task'
```
