# Architecture

RushChat system architecture and technology stack.

## System Architecture Overview

```markmap
# RushChat System Architecture
## Frontend Layer
- React 18
  - Socket.io Client
  - CSS Variables
  - React Context
- Feature Modules
  - Real-time Chat
  - Channel Management
  - User System
  - Wallet Connection
## Backend Layer
- Rust + Axum
  - WebSocket Service
  - REST API
  - File Upload
- Core Functions
  - Message Processing
  - User Authentication
  - Channel Management
  - Wallet Verification
## Data Layer
- MySQL Database
  - User Data
  - Message Storage
  - Channel Information
  - Session Management
## External Services
- Blockchain RPC
  - EVM Chains
  - Solana Chain
- Smart Contracts
  - Red Packet Contracts
  - X402 Protocol
```

## System Architecture

```
┌─────────────────┐
│   React Frontend│
│  (Port 3000)    │
└────────┬────────┘
         │ HTTP/WebSocket
         │
┌────────▼────────┐
│  Rust Backend   │
│  (Port 5001)    │
│  - Axum         │
│  - WebSocket    │
│  - REST API     │
└────────┬────────┘
         │
┌────────▼────────┐
│   MySQL Database│
│  (Port 3306)    │
└─────────────────┘
```

## Technology Stack

### Backend

- **Rust** - Systems programming language, high performance
- **Axum** - Modern async web framework
- **Tokio** - Async runtime
- **SQLx** - Type-safe async SQL toolkit (MySQL)
- **Serde** - Serialization/deserialization
- **Bcrypt** - Password encryption

### Frontend

- **React 18** - UI framework
- **Socket.io Client** - WebSocket communication
- **CSS Variables** - Theme system
- **React Context** - State management

### Database

- **MySQL 5.7+** - Relational database
- **utf8mb4** - Character set, supports emoji

## Core Modules

### Backend Modules

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
```

### Frontend Modules

```
client/
├── src/
│   ├── App.js               # Main application component
│   ├── index.js             # Entry point
│   ├── components/          # React components
│   │   ├── ChatRoom.js
│   │   ├── ChannelManager.js
│   │   ├── MessageList.js
│   │   └── ...
│   ├── utils/               # Utility functions
│   │   ├── websocket.js
│   │   ├── wallet.js
│   │   └── ...
│   ├── i18n/                # Internationalization
│   └── config/              # Configuration files
```

## Data Flow

### Message Sending Flow

```
User Input Message
    ↓
Frontend Component Processing
    ↓
WebSocket Send (message:send)
    ↓
Backend WebSocket Handler
    ↓
Database Save
    ↓
Broadcast to All Online Users
    ↓
Frontend Receive and Display
```

### User Authentication Flow

```
User Login
    ↓
POST /api/auth/login
    ↓
Backend Verify Password
    ↓
Generate Session
    ↓
Return User Information
    ↓
Frontend Save Session
    ↓
WebSocket Connection
```

## Performance Optimization

### Backend Optimization

- Use connection pool to manage database connections
- Async I/O processing
- Broadcast channels for WebSocket message distribution
- Type-safe database queries

### Frontend Optimization

- React component lazy loading
- Message list virtual scrolling (planned)
- Image compression and caching
- WebSocket auto-reconnect

## Security Features

- Password encrypted storage (bcrypt)
- CORS configuration
- SQL injection protection (SQLx type safety)
- XSS protection (React auto-escaping)
- IP banning mechanism
- User muting mechanism

## Scalability

### Horizontal Scaling

- Stateless backend design
- Database connection pool
- WebSocket connection management

### Vertical Scaling

- Rust high performance
- Async processing
- Database index optimization

## Related Documentation

- [API Documentation](api.md)
- [WebSocket Events](websocket.md)
- [Database Design](database.md)
