# Configuration

RushChat configuration is primarily done through environment variables.

## Configuration Overview

```markmap
# Configuration
## Backend Configuration
- Basic Services
  - PORT: 5001
  - NODE_ENV
  - CLIENT_URL
  - MAIN_DOMAIN
- Database Configuration
  - DB_HOST
  - DB_PORT
  - DB_USER
  - DB_PASSWORD
  - DB_NAME
- Solana RPC
  - SOL_HTTP_RPC
  - SOL_RPC
  - SOL_MAINNET_RPC
- Red Packet Contracts
  - RED_PACKET_CONTRACT_ADDRESS
  - SOLANA_RED_PACKET_PROGRAM_ID
## Frontend Configuration
- API Address
  - REACT_APP_API_URL
- WebSocket Address
  - REACT_APP_SOCKET_URL
## Configuration Files
- .env File
  - Project Root Directory
  - Backend Loads First
- Environment Template
  - docs/ENVIRONMENT_TEMPLATE.md
  - Can Copy and Use
## Configuration Verification
- Database Connection
- Port Check
- CORS Configuration
```

## Environment Variables

### Backend Configuration

Create a `.env` file in the project root directory (backend will prioritize loading the `.env` file in the project root).

#### Basic Services

```env
PORT=5001                    # Backend service port
NODE_ENV=development         # Environment mode: development | production
CLIENT_URL=http://localhost:3000  # Frontend address (for CORS)
MAIN_DOMAIN=localhost        # Main domain (set to actual domain in production)
```

#### Database

```env
DB_HOST=localhost            # Database host
DB_PORT=3306                 # Database port
DB_USER=root                 # Database username
DB_PASSWORD=your_password    # Database password
DB_NAME=rushchat             # Database name
```

#### Solana RPC (Optional)

```env
SOL_HTTP_RPC=https://api.mainnet-beta.solana.com
SOL_RPC=https://api.mainnet-beta.solana.com
```

#### Red Packet Contracts (Optional)

```env
# EVM chain red packet contract address
RED_PACKET_CONTRACT_ADDRESS=

# Solana red packet program ProgramId (Base58, typically 32~44 characters)
# Important: Must be "Program ProgramId", not wallet address
SOLANA_RED_PACKET_PROGRAM_ID=
```

### Frontend Configuration

Create a `.env` file in the `client/` directory:

```env
REACT_APP_API_URL=http://localhost:5001
REACT_APP_SOCKET_URL=http://localhost:5001
```

## Configuration Files

### Database Configuration

Database configuration is read from environment variables, no additional configuration file needed.

### Channel Rules Configuration

Channel rules are stored in the database and configured through the admin interface or API.

## Production Environment Configuration

### Railway Deployment

Configure environment variables in Railway project settings:

```env
DB_HOST=<railway_mysql_host>
DB_PORT=3306
DB_USER=<railway_mysql_user>
DB_PASSWORD=<railway_mysql_password>
DB_NAME=<railway_mysql_database>
PORT=5001
NODE_ENV=production
CLIENT_URL=https://your-app.vercel.app
MAIN_DOMAIN=your-domain.com
```

### Vercel Deployment

Configure environment variables in Vercel project settings:

```env
REACT_APP_API_URL=https://your-backend.railway.app
REACT_APP_SOCKET_URL=https://your-backend.railway.app
```

## Security Configuration

### CORS Configuration

Backend controls CORS allowed origins through the `CLIENT_URL` environment variable.

### Database Security

- Use strong passwords
- Restrict database access IP
- Regularly backup database

### Production Environment Recommendations

- Use HTTPS
- Set strong password policy
- Enable database SSL connection
- Configure firewall rules

## Environment Variable Priority

Backend environment variable loading order:

1. Project root directory `.env` file
2. System environment variables
3. Default values

## Configuration Verification

### Check Environment Variables

```bash
# Backend
cd server-rust
cargo run -- --check-env

# Frontend
cd client
npm run check-env
```

### Test Database Connection

```bash
mysql -u $DB_USER -p$DB_PASSWORD -h $DB_HOST -P $DB_PORT $DB_NAME -e "SELECT 1;"
```

## Common Configuration Issues

### CORS Error

Ensure `CLIENT_URL` includes protocol (`http://` or `https://`)

### Database Connection Failed

Check database credentials and network connection

### Port Conflict

Change `PORT` environment variable and update frontend `REACT_APP_SOCKET_URL`

## References

- [Environment Variable Template](https://github.com/Yukitojp/RustChat/blob/main/docs/ENVIRONMENT_TEMPLATE.md)
- [Deployment Guide](deployment/overview.md)
