# Development Environment

Detailed instructions for setting up RushChat development environment.

## Development Environment Overview

```markmap
# Development Environment Setup
## Required Software
- Node.js
  - Version ≥ 18
  - npm/pnpm
- Rust
  - Version ≥ 1.70
  - cargo
- MySQL
  - Version ≥ 5.7
  - MariaDB ≥ 10.3
- Git
  - Version Control
## Recommended Tools
- Code Editor
  - VS Code
  - Cursor
- Database Management
  - MySQL Workbench
  - DBeaver
- API Testing
  - Postman
  - Insomnia
## Installation Steps
- Install Node.js
  - nvm Installation
  - Official Website Download
- Install Rust
  - rustup Installation
  - Verify Version
- Install MySQL
  - macOS: brew
  - Ubuntu: apt
  - Windows: Official Website
- Clone Project
  - git clone
  - Enter Directory
- Install Dependencies
  - npm install
  - cargo build
- Database Setup
  - Create Database
  - Run Migrations
- Configure Environment
  - .env File
  - Environment Variables
## Verify Installation
- Check Database
  - Connection Test
  - Table Structure Verification
- Check Rust
  - cargo check
  - Compilation Test
- Check Frontend
  - npm list
  - Dependency Verification
```

## Prerequisites

### Required Software

- **Node.js** ≥ 18
- **Rust** ≥ 1.70
- **MySQL** ≥ 5.7 or **MariaDB** ≥ 10.3
- **Git**

### Recommended Tools

- **VS Code** or **Cursor** - Code editor
- **MySQL Workbench** - Database management
- **Postman** - API testing

## Environment Setup

### 1. Install Node.js

```bash
# Using nvm (recommended)
nvm install 20
nvm use 20

# Or download from official website
# https://nodejs.org/
```

### 2. Install Rust

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env
rustc --version
```

### 3. Install MySQL

#### macOS

```bash
brew install mysql
brew services start mysql
```

#### Ubuntu/Debian

```bash
sudo apt-get update
sudo apt-get install mysql-server
sudo systemctl start mysql
```

### 4. Clone Project

```bash
git clone <repository-url>
cd RushChat
```

### 5. Install Dependencies

```bash
# Root directory dependencies
npm install

# Client dependencies
cd client && npm install && cd ..
```

### 6. Database Setup

```bash
# Create database
mysql -u root -p < database/schema.sql
```

### 7. Configure Environment Variables

Create `.env` file:

```env
DB_HOST=localhost
DB_PORT=3306
DB_USER=root
DB_PASSWORD=your_password
DB_NAME=rushchat
PORT=5001
NODE_ENV=development
CLIENT_URL=http://localhost:3000
REACT_APP_SOCKET_URL=http://localhost:5001
```

## Start Development Server

### Backend

```bash
cd server-rust
cargo run
```

### Frontend

```bash
cd client
npm start
```

## Development Tools

### VS Code Extensions

Recommended installations:

- Rust Analyzer
- ESLint
- Prettier
- MySQL

### Debug Configuration

Create `.vscode/launch.json`:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "lldb",
      "request": "launch",
      "name": "Debug Rust Server",
      "cargo": {
        "args": ["build", "--bin=rushchat-server"],
        "filter": {
          "name": "rushchat-server",
          "kind": "bin"
        }
      },
      "args": [],
      "cwd": "${workspaceFolder}/server-rust"
    }
  ]
}
```

## Related Documentation

- [Code Structure](structure.md)
- [Contributing Guide](contributing.md)
