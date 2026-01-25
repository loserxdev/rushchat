# Environment Variables

RushChat environment variable configuration documentation.

## Environment Variables Overview

```markmap
# Environment Variable Configuration
## Backend Environment Variables
- Database Configuration
  - DB_HOST
  - DB_PORT
  - DB_USER
  - DB_PASSWORD
  - DB_NAME
- Server Configuration
  - PORT
  - NODE_ENV
  - CLIENT_URL
  - MAIN_DOMAIN
- Solana Configuration
  - SOL_HTTP_RPC
  - SOL_RPC
  - SOL_MAINNET_RPC
  - SOLANA_RED_PACKET_PROGRAM_ID
- EVM Configuration
  - RED_PACKET_CONTRACT_ADDRESS
  - BSC_RPC_URL
  - ETH_RPC_URL
## Frontend Environment Variables
- API Configuration
  - REACT_APP_API_URL
  - REACT_APP_SOCKET_URL
## Configuration Methods
- .env File
  - Project Root Directory
  - Development Environment
- Platform Configuration
  - Railway Environment Variables
  - Vercel Environment Variables
  - Production Environment
```

## Backend Environment Variables

### Database Configuration

```env
DB_HOST=localhost              # Database host
DB_PORT=3306                   # Database port
DB_USER=root                   # Database username
DB_PASSWORD=your_password      # Database password
DB_NAME=rushchat               # Database name
```

### Server Configuration

```env
PORT=5001                      # Service port
NODE_ENV=production            # Environment mode
CLIENT_URL=https://your-app.vercel.app  # Frontend address (CORS)
MAIN_DOMAIN=your-domain.com    # Main domain
```

### Solana Configuration (Optional)

```env
SOL_HTTP_RPC=https://api.mainnet-beta.solana.com
SOL_RPC=https://api.mainnet-beta.solana.com
SOL_MAINNET_RPC=https://rozanna-srqsog-fast-mainnet.helius-rpc.com
SOLANA_RED_PACKET_PROGRAM_ID=your_program_id
```

### EVM Configuration (Optional)

```env
RED_PACKET_CONTRACT_ADDRESS=0x...
BSC_RPC_URL=https://bsc-dataseed.binance.org/
ETH_RPC_URL=https://eth.llamarpc.com
```

## Frontend Environment Variables

### API Configuration

```env
REACT_APP_API_URL=https://your-backend.railway.app
REACT_APP_SOCKET_URL=https://your-backend.railway.app
```

## Railway Environment Variables

Railway uses template variables to reference database:

```env
DB_HOST=${{MySQL.MYSQLHOST}}
DB_PORT=${{MySQL.MYSQLPORT}}
DB_USER=${{MySQL.MYSQLUSER}}
DB_PASSWORD=${{MySQL.MYSQLPASSWORD}}
DB_NAME=${{MySQL.MYSQLDATABASE}}
```

## Vercel Environment Variables

Configure in Vercel project settings:

- All `REACT_APP_*` variables
- Distinguish production, preview, development environments

## Security Recommendations

### Production Environment

- Use strong passwords
- Regularly rotate keys
- Restrict database access IP
- Enable SSL/TLS

### Environment Variable Management

- Do not commit `.env` to Git
- Use environment variable management tools
- Regularly review environment variables

## Related Documentation

- [Configuration](../configuration.md)
- [Railway Deployment](railway.md)
- [Vercel Deployment](vercel.md)
