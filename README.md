# Rust Axum Backend

This project is a backend API built with [Axum](https://github.com/tokio-rs/axum), a web application framework for Rust. It provides endpoints for creating and managing "Capsules"—messages that can be unlocked at a specified time and optionally trigger email notifications.

## Features

- Create time-locked capsules with a name, email, title, and message
- Unlock capsules at a specified date/time
- Email notification support
- RESTful API design
- Input validation using `validator`
- Uses PostgreSQL (or other SQL DB) via `sqlx`
- UUID-based public and internal IDs

## Project Structure

```
backend/
├── Cargo.toml
├── migrations/           # SQL migration files
├── src/
│   ├── config.rs         # Configuration management
│   ├── db.rs             # Database logic
│   ├── dtos.rs           # Data transfer objects (DTOs)
│   ├── error.rs          # Error handling
│   ├── handler.rs        # HTTP request handlers
│   └── main.rs           # Application entry point
└── target/               # Build output (auto-generated)
```

## Getting Started

### Prerequisites

- [Rust](https://www.rust-lang.org/tools/install)
- [PostgreSQL](https://www.postgresql.org/) (or compatible SQL database)

### Setup

1. **Clone the repository:**
   ```sh
   git clone <repo-url>
   cd backend
   ```
2. **Configure environment variables:**
   - Create a `.env` file or set environment variables as needed (see `config.rs` for details).
3. **Run database migrations:**
   ```sh
   cargo install sqlx-cli --no-default-features --features native-tls,postgres
   sqlx migrate run
   ```
4. **Build and run the server:**
   ```sh
   cargo run
   ```

## API Overview

### Create Capsule

- **Endpoint:** `POST /capsules`
- **Request Body:**
  ```json
  {
    "name": "John Doe",
    "email": "john@example.com",
    "title": "My Capsule",
    "message": "Hello future!",
    "unlock_at": "2026-12-31T23:59:59Z"
  }
  ```
- **Response:**
  ```json
  {
    "public_id": "...",
    "unlock_at": "2026-12-31T23:59:59Z"
  }
  ```

### Get Capsule

- **Endpoint:** `GET /capsules/{public_id}`
- **Response:**
  ```json
  {
    "id": "...",
    "public_id": "...",
    "name": "...",
    "title": "...",
    "message": "...",
    "unlock_at": "...",
    "created_at": "...",
    "is_unlocked": true
  }
  ```

## Technologies Used

- [Axum](https://github.com/tokio-rs/axum)
- [Tokio](https://tokio.rs/)
- [SQLx](https://github.com/launchbadge/sqlx)
- [Serde](https://serde.rs/)
- [Validator](https://github.com/Keats/validator)
- [UUID](https://docs.rs/uuid/)
- [Chrono](https://docs.rs/chrono/)

## License

MIT
