# Installation Guide

Detailed installation and configuration instructions.

## Installation Process Overview

```markmap
# Installation Guide
## System Requirements
- Required Software
  - Node.js ≥ 18
  - Rust ≥ 1.70
  - MySQL ≥ 5.7
  - Git
- Recommended Tools
  - npm/pnpm
  - cargo
## Installation Steps
- Install Node.js
  - Official Website Download
  - nvm Installation
  - Verify Version
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
  - cd client && npm install
- Database Setup
  - Create Database
  - Run Migrations
- Configure Environment Variables
  - Create .env File
  - Set Database
  - Configure Port
- Verify Installation
  - Check Database
  - Check Rust Compilation
  - Check Frontend Dependencies
## Run Modes
- Development Mode
  - cargo run
  - npm start
- Production Mode
  - cargo build --release
  - npm run build
```

## System Requirements

### Required

- **Node.js** ≥ 18
- **Rust** ≥ 1.70 (install using `rustup`)
- **MySQL** ≥ 5.7 or **MariaDB** ≥ 10.3
- **Git**

### Recommended

- **npm** or **pnpm** package manager
- **cargo** (Rust package manager, installed with Rust)

## Installation Steps

### 1. Install Node.js

Visit the [Node.js official website](https://nodejs.org/) to download and install.

Verify installation:

```bash
node --version  # Should show v18 or higher
npm --version
```

### 2. Install Rust

Install using `rustup`:

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Verify installation:

```bash
rustc --version  # Should show 1.70 or higher
cargo --version
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

#### Windows

Download the installer from the [MySQL official website](https://dev.mysql.com/downloads/mysql/).

### 4. Clone Project

```bash
git clone <repository-url>
cd RushChat
```

### 5. Install Project Dependencies

```bash
# Install root directory dependencies
npm install

# Install client dependencies
cd client && npm install && cd ..
```

### 6. Database Setup

#### Create Database

```bash
mysql -u root -p < database/schema.sql
```

#### Run Migrations (if database already exists)

```bash
mysql -u root -p rushchat < database/complete_schema_latest.sql
```

### 7. Configure Environment Variables

Create a `.env` file in the project root directory:

```env
# Basic Services
PORT=5001
NODE_ENV=development
CLIENT_URL=http://localhost:3000

# Database
DB_HOST=localhost
DB_PORT=3306
DB_USER=root
DB_PASSWORD=your_password
DB_NAME=rushchat

# WebSocket
REACT_APP_SOCKET_URL=http://localhost:5001

# Red Packet Contracts (Optional)
RED_PACKET_CONTRACT_ADDRESS=
SOLANA_RED_PACKET_PROGRAM_ID=
```

> 💡 Tip: You can copy `docs/ENVIRONMENT_TEMPLATE.md` as a template

### 8. Verify Installation

#### Check Database Connection

```bash
mysql -u root -p -e "USE rushchat; SHOW TABLES;"
```

You should see the following tables:
- users
- messages
- channels
- sessions
- etc...

#### Check Rust Compilation

```bash
cd server-rust
cargo check
```

#### Check Frontend Dependencies

```bash
cd client
npm list --depth=0
```

## Run in Development Mode

### Start Backend

```bash
cd server-rust
cargo run
```

### Start Frontend

```bash
cd client
npm start
```

## Build for Production

### Build Backend

```bash
cd server-rust
cargo build --release
./target/release/rushchat-server
```

### Build Frontend

```bash
cd client
npm run build
```

Build artifacts are in the `client/build/` directory.

## Next Steps

- 📖 Read [Getting Started](getting-started.md)
- 🔧 Check [Configuration](configuration.md)
- 🚀 Check [Deployment Guide](deployment/overview.md)
