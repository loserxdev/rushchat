# Rust Backend

RushChat's backend is written in Rust, based on the Axum framework.

## Rust Backend Overview

```markmap
# Rust Backend
## Technology Stack
- Rust
  - Systems Programming Language
  - High Performance
  - Memory Safe
- Axum
  - Async Web Framework
  - Routing System
  - Middleware
- Tokio
  - Async Runtime
  - Task Scheduling
- SQLx
  - Type-safe SQL
  - MySQL Driver
  - Async Queries
- Serde
  - Serialization/Deserialization
  - JSON Processing
- Bcrypt
  - Password Encryption
  - Secure Storage
## Project Structure
- models/
  - user.rs
  - message.rs
  - channel.rs
  - Data Models
- handlers/
  - auth.rs
  - user.rs
  - channel.rs
  - HTTP Handlers
- websocket/
  - connection.rs
  - events.rs
  - state.rs
  - Real-time Communication
- utils/
  - rpc.rs
  - permissions.rs
  - Utility Functions
## Core Functions
- WebSocket Communication
  - Real-time Messages
  - Broadcast Mechanism
  - Connection Management
- REST API
  - User Authentication
  - Resource Management
  - File Upload
- Database Operations
  - Type Safety
  - Connection Pool
  - Transaction Support
```

## Technology Stack

- **Rust** - Systems programming language
- **Axum** - Modern async web framework
- **Tokio** - Async runtime
- **SQLx** - Type-safe async SQL toolkit (MySQL)
- **Serde** - Serialization/deserialization
- **Bcrypt** - Password encryption

## Project Structure

```
server-rust/
├── src/
│   ├── main.rs              # Entry point
│   ├── config.rs            # Configuration management
│   ├── db.rs                # Database connection
│   ├── models/              # Data models
│   │   ├── user.rs
│   │   ├── message.rs
│   │   ├── channel.rs
│   │   └── ...
│   ├── handlers/            # HTTP handlers
│   │   ├── auth.rs
│   │   ├── user.rs
│   │   ├── channel.rs
│   │   └── ...
│   ├── websocket/           # WebSocket handlers
│   │   ├── connection.rs
│   │   ├── events.rs
│   │   └── state.rs
│   └── utils/               # Utility functions
│       ├── rpc.rs           # RPC utilities (NFT verification, etc.)
│       └── permissions.rs
├── Cargo.toml
└── README.md
```

## Core Functions

### WebSocket Real-time Communication

- Based on Tokio WebSocket
- Supports broadcast messages
- Connection management and heartbeat detection

### RESTful API

- User authentication
- User management
- Channel management
- Message management
- File upload

### Database Integration

- Uses SQLx for type-safe queries
- Connection pool management
- Async database operations

### File Upload

- Avatar upload
- Sticker upload
- Image compression

## Development

### Run Development Server

```bash
cd server-rust
cargo run
```

### Build Production Version

```bash
cargo build --release
```

### Run Tests

```bash
cargo test
```

## Performance Optimization

- Use connection pool to manage database connections
- Async I/O processing
- Broadcast channels for WebSocket message distribution
- Type-safe database queries

## Related Documentation

- [Architecture](architecture.md)
- [API Documentation](api.md)
- [Database Design](database.md)
