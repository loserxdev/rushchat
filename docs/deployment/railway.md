# Railway Deployment

Deploy RushChat backend service using Railway.

## Railway Deployment Overview

```markmap
# Railway Deployment
## Prerequisites
- Railway Account
- GitHub Account
- Code Pushed
## Deployment Steps
- Create Project
  - New Project
  - Deploy from GitHub
  - Select server-rust Directory
- Add Database
  - New → Database → MySQL
  - Auto Create
  - Record Connection Info
- Configure Environment Variables
  - DB_HOST
  - DB_PORT
  - DB_USER
  - DB_PASSWORD
  - DB_NAME
  - PORT
  - CLIENT_URL
- Configure Build
  - Build Command
  - Start Command
  - Root Directory
## Database Migration
- Run Migration Scripts
- Verify Table Structure
- Check Data
## Verify Deployment
- Check Service Status
- Test API Endpoints
- Check Logs
```

## Prerequisites

- Railway account (https://railway.app/)
- GitHub account
- Code pushed to GitHub

## Deployment Steps

### 1. Create Railway Project

1. Log in to Railway
2. Click "New Project"
3. Select "Deploy from GitHub repo"
4. Select RushChat repository
5. Select `server-rust` directory as Root Directory

### 2. Add MySQL Database

1. Click "New" on project page
2. Select "Database" → "MySQL"
3. Railway will automatically create database
4. Record database connection information

### 3. Configure Environment Variables

Add environment variables in project settings:

```env
DB_HOST=${{MySQL.MYSQLHOST}}
DB_PORT=${{MySQL.MYSQLPORT}}
DB_USER=${{MySQL.MYSQLUSER}}
DB_PASSWORD=${{MySQL.MYSQLPASSWORD}}
DB_NAME=${{MySQL.MYSQLDATABASE}}
PORT=5001
NODE_ENV=production
CLIENT_URL=https://your-frontend.vercel.app
MAIN_DOMAIN=your-domain.com
```

### 4. Configure Build Commands

Railway automatically detects Rust projects, but can be manually configured:

**Build Command**:
```bash
cargo build --release
```

**Start Command**:
```bash
./target/release/rushchat-server
```

### 5. Run Database Migration

1. On Railway project page
2. Open MySQL database
3. Use Railway CLI or MySQL client
4. Run migration script:

```bash
mysql -h $MYSQLHOST -u $MYSQLUSER -p$MYSQLPASSWORD $MYSQLDATABASE < database/schema.sql
```

### 6. Configure Persistent Storage

Railway uses temporary file system, need to configure Volume:

1. Add Volume in project settings
2. Mount to `/app/uploads` directory
3. Used for storing uploaded files

### 7. Configure Domain

1. In project settings
2. Click "Generate Domain"
3. Or add custom domain
4. Update frontend environment variables

## Monitoring and Logs

### View Logs

1. On Railway project page
2. Click "Deployments"
3. Select latest deployment
4. View real-time logs

### Monitoring Metrics

Railway provides:

- CPU usage
- Memory usage
- Network traffic
- Request count

## Troubleshooting

### Build Failed

- Check Rust version
- Check if dependencies are correct
- View build logs

### Runtime Errors

- Check environment variables
- Check database connection
- View application logs

### Database Connection Failed

- Check if database service is running
- Check if environment variables are correct
- Check network connection

## Related Documentation

- [Deployment Overview](overview.md)
- [Environment Variables](environment.md)
