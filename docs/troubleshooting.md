# Troubleshooting

Common problems and solutions.

## Troubleshooting Overview

```markmap
# Troubleshooting
## Database Issues
- Connection Failed
  - Check MySQL Running
  - Check .env Configuration
  - Verify Database
  - Check Permissions
- Migration Failed
  - Check Version
  - Check Syntax
  - View Logs
  - Manual Execution
## Network Issues
- WebSocket Connection Failed
  - Check Backend
  - Check Configuration
  - Check Firewall
  - Check CORS
- CORS Error
  - Check CLIENT_URL
  - Ensure HTTPS
  - Check Domain
  - Check Nginx
## Compilation Issues
- Rust Compilation Error
  - Check Version
  - Update Dependencies
  - Clean Build
- Frontend Build Error
  - Check Node Version
  - Clean node_modules
  - Reinstall
## Runtime Issues
- Service Startup Failed
  - Check Port
  - Check Configuration
  - View Logs
- Function Abnormal
  - Check Database
  - Check Network
  - View Logs
```

## Database Issues

### Database Connection Failed

**Problem**: Unable to connect to database

**Solution**:
1. Check if MySQL is running: `sudo systemctl status mysql`
2. Check database credentials in `.env` file
3. Verify database exists: `mysql -u root -p -e "SHOW DATABASES;"`
4. Check database user permissions

### Database Migration Failed

**Problem**: Error when running migration script

**Solution**:
1. Check if database version is compatible
2. Check migration script syntax
3. View error logs
4. Manually execute SQL statements

## Network Issues

### WebSocket Connection Failed

**Problem**: Unable to establish WebSocket connection

**Solution**:
1. Check if backend service is running
2. Check `REACT_APP_SOCKET_URL` configuration
3. Check firewall rules
4. Check CORS configuration

### CORS Error

**Problem**: Browser console shows CORS error

**Solution**:
1. Check backend `CLIENT_URL` environment variable
2. Ensure frontend address includes protocol (`https://`)
3. Check if domain matches
4. Check Nginx configuration (if using)

## Compilation Issues

### Rust Compilation Error

**Problem**: `cargo build` fails

**Solution**:
1. Check Rust version: `rustc --version`
2. Update Rust: `rustup update`
3. Clean build cache: `cargo clean`
4. Check if dependencies are correct

### Frontend Build Error

**Problem**: `npm run build` fails

**Solution**:
1. Check Node.js version: `node --version`
2. Delete `node_modules` and reinstall
3. Check dependency version conflicts
4. View build logs

## Runtime Issues

### Port Already in Use

**Problem**: Service startup failed, port is occupied

**Solution**:
1. Find process using the port: `lsof -i :5001`
2. Stop the process using the port
3. Or change `PORT` in `.env`

### File Upload Failed

**Problem**: Unable to upload files

**Solution**:
1. Check file size limit
2. Check directory permissions
3. Check disk space
4. Railway requires Volume configuration

## Wallet Issues

### Wallet Connection Failed

**Problem**: Unable to connect wallet

**Solution**:
1. Check if wallet extension is installed
2. Check if wallet is unlocked
3. Check network configuration
4. View browser console errors

### Transaction Failed

**Problem**: On-chain transaction failed

**Solution**:
1. Check wallet balance
2. Check Gas fees
3. Check network connection
4. View transaction details

## Performance Issues

### Slow Response

**Problem**: Application responds slowly

**Solution**:
1. Check database connection pool configuration
2. Check network latency
3. Check server resources
4. Optimize database queries

### High Memory Usage

**Problem**: Server memory usage is high

**Solution**:
1. Check connection count
2. Check for memory leaks
3. Optimize code
4. Increase server memory

## Getting Help

If the problem is still not resolved:

1. Check [FAQ](faq.md)
2. Check GitHub Issues
3. Submit a new Issue
4. Contact maintainers

## Related Documentation

- [FAQ](faq.md)
- [Development Environment](development/setup.md)
