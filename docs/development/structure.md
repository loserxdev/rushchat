# Code Structure

RushChat project code structure documentation.

## Code Structure Overview

```markmap
# Code Structure
## Project Structure
- server-rust/
  - Rust Backend
  - Cargo.toml
  - src/
- client/
  - React Frontend
  - package.json
  - src/
- database/
  - schema.sql
  - migration_*.sql
- docs/
  - Project Documentation
- gitbook/
  - GitBook Documentation
## Backend Structure
- models/
  - Data Models
  - CRUD Operations
- handlers/
  - HTTP Handlers
  - Route Handling
- websocket/
  - WebSocket Handling
  - Event Handling
- utils/
  - Utility Functions
  - RPC Utilities
## Frontend Structure
- components/
  - React Components
  - UI Components
- utils/
  - Utility Functions
  - WebSocket
  - Wallet
- i18n/
  - Internationalization
  - Multi-language
- config/
  - Configuration Files
  - Wagmi Configuration
```

## Project Structure

```
RushChat/
├── server-rust/           # Rust Backend
│   ├── src/
│   │   ├── main.rs
│   │   ├── config.rs
│   │   ├── db.rs
│   │   ├── models/       # Data models
│   │   ├── handlers/     # HTTP handlers
│   │   ├── websocket/    # WebSocket handlers
│   │   └── utils/        # Utility functions
│   └── Cargo.toml
├── client/                # React Frontend
│   ├── src/
│   │   ├── components/   # React components
│   │   ├── utils/        # Utility functions
│   │   ├── i18n/         # Internationalization
│   │   └── config/       # Configuration files
│   └── package.json
├── database/              # Database files
│   ├── schema.sql
│   └── migration_*.sql
├── docs/                  # Documentation
└── gitbook/              # GitBook documentation
```

## Backend Structure

### models/

Data models, containing CRUD operations for all database tables:

- `user.rs` - User model
- `message.rs` - Message model
- `channel.rs` - Channel model
- `ban.rs` - Ban model
- etc...

### handlers/

HTTP request handlers:

- `auth.rs` - Authentication related
- `user.rs` - User related
- `channel.rs` - Channel related
- `message.rs` - Message related
- etc...

### websocket/

WebSocket connection and event handling:

- `connection.rs` - Connection management
- `events.rs` - Event handling
- `state.rs` - State management

### utils/

Utility functions:

- `rpc.rs` - RPC utilities (NFT verification, etc.)
- `permissions.rs` - Permission checking

## Frontend Structure

### components/

React components:

- `ChatRoom.js` - Chat room
- `ChannelManager.js` - Channel management
- `MessageList.js` - Message list
- `WalletConnect.jsx` - Wallet connection
- etc...

### utils/

Utility functions:

- `websocket.js` - WebSocket connection
- `wallet.js` - Wallet utilities
- `contract.js` - Contract interaction

### i18n/

Internationalization:

- `index.js` - i18n configuration
- `locales/zh.js` - Chinese translations
- `locales/en.js` - English translations

## Code Standards

### Rust

- Use `rustfmt` for formatting
- Use `clippy` for checking
- Follow Rust best practices

### JavaScript

- Use ESLint
- Use Prettier
- Follow React best practices

## Related Documentation

- [Development Environment](setup.md)
- [Contributing Guide](contributing.md)
