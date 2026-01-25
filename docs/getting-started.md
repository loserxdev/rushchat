# Getting Started

This guide will help you get RushChat up and running in 5 minutes.

## Getting Started Overview

```markmap
# Getting Started Guide
## Prerequisites
- Node.js ≥ 18
- Rust ≥ 1.70
- MySQL ≥ 5.7
- Git
## Installation Steps
- Clone Project
  - git clone
  - Enter Directory
- Install Dependencies
  - npm install
  - cd client && npm install
- Database Setup
  - Create Database
  - Import Schema
- Configure Environment
  - Create .env File
  - Set Database Connection
  - Configure Port and URL
- Start Application
  - Start Backend
  - Start Frontend
## Start Services
- Backend Service
  - cd server-rust
  - cargo run
  - Port 5001
- Frontend Service
  - cd client
  - npm start
  - Port 3000
## Verify Installation
- Check Backend
  - Health Check Endpoint
  - Port Listening
- Check Frontend
  - Page Loading
  - Chat Interface
  - Guest Mode
## Next Steps
- Read User Guide
- Check Configuration
- Deploy to Production
```

## Prerequisites

- **Node.js** ≥ 18
- **Rust** ≥ 1.70
- **MySQL** ≥ 5.7 or **MariaDB** ≥ 10.3
- **Git**

## Installation Steps

### 1. Clone Project

```bash
git clone <repository-url>
cd RushChat
```

### 2. Install Dependencies

```bash
# Install root directory dependencies
npm install

# Install client dependencies
cd client && npm install && cd ..
```

### 3. Database Setup

#### Create Database

```bash
mysql -u root -p < database/schema.sql
```

Or execute manually:

```sql
mysql -u root -p
source database/schema.sql
```

#### Configure Database Connection

Create a `.env` file in the project root directory:

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

> 💡 Tip: You can copy `docs/ENVIRONMENT_TEMPLATE.md` as a template

### 4. Start Application

#### Start Backend (Rust)

```bash
cd server-rust
cargo run
```

The backend server will run at: `http://localhost:5001`

#### Start Frontend (React)

Open a new terminal window:

```bash
cd client
npm start
```

The React development server will run at: `http://localhost:3000`

### 5. Access Application

Open your browser and visit: `http://localhost:3000`

## Verify Installation

### Check Backend

Visit `http://localhost:5001/api/health` (if health check endpoint is configured)

### Check Frontend

- Page loads normally
- Chat interface is visible
- Can enter as guest

## Next Steps

- 📖 Read [User Guide](user-guide/user-system.md) to learn how to use
- 🔧 Check [Configuration](configuration.md) for detailed configuration
- 🚀 Check [Deployment Guide](deployment/overview.md) to deploy to production

## Common Issues

### Database Connection Failed

- Ensure MySQL is running
- Check database credentials in `.env` file
- Verify database exists: `mysql -u root -p -e "SHOW DATABASES;"`

### Port Already in Use

- Change `PORT` in `.env` file
- Update `REACT_APP_SOCKET_URL` in client

### CORS Error

- Check backend `CLIENT_URL` environment variable
- Ensure frontend address includes protocol (`http://` or `https://`)

## Need Help?

- 📖 Check [FAQ](faq.md)
- 🔍 Check [Troubleshooting](troubleshooting.md)
- 📝 Check [Full Documentation](README.md)
