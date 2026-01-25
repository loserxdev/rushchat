# Nginx Configuration

Configuration documentation for using Nginx as a reverse proxy.

## Nginx Configuration Overview

```markmap
# Nginx Configuration
## Basic Configuration
- HTTP Redirect
  - Port 80 Listen
  - 301 Redirect to HTTPS
- HTTPS Configuration
  - Port 443
  - SSL Certificate
  - HTTP/2 Support
## Reverse Proxy
- API Proxy
  - /api Path
  - Proxy to Backend
  - Request Headers
- WebSocket Proxy
  - /ws Path
  - Upgrade Header
  - Connection Header
- Static Files
  - Frontend Build Files
  - Static Resources
## SSL Configuration
- Certificate Configuration
  - ssl_certificate
  - ssl_certificate_key
- Security Configuration
  - TLS Protocol
  - Cipher Suites
  - Security Headers
## Performance Optimization
- Cache Configuration
- Compression Configuration
- Connection Pool
```

## Basic Configuration

### HTTP to HTTPS Redirect

```nginx
server {
    listen 80;
    server_name your-domain.com;
    return 301 https://$server_name$request_uri;
}
```

### HTTPS Configuration

```nginx
server {
    listen 443 ssl http2;
    server_name your-domain.com;

    ssl_certificate /path/to/cert.pem;
    ssl_certificate_key /path/to/key.pem;

    # SSL Configuration
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;
    ssl_prefer_server_ciphers on;

    # Proxy to Backend
    location /api {
        proxy_pass http://localhost:5001;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    # WebSocket Support
    location /ws {
        proxy_pass http://localhost:5001;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        
        # WebSocket Timeout Settings
        proxy_read_timeout 86400;
    }

    # Static Files (Frontend)
    location / {
        root /path/to/client/build;
        try_files $uri $uri/ /index.html;
    }

    # File Upload
    client_max_body_size 10M;
}
```

## Complete Configuration Example

Refer to `docs/nginx-config-example.conf` for complete configuration.

## Troubleshooting

### 301 Redirect Loop

Check:

- SSL certificate configuration
- Proxy settings
- Domain configuration

### WebSocket Connection Failed

Ensure:

- Correctly configure `Upgrade` and `Connection` headers
- Set sufficient timeout
- Check firewall rules

### File Upload Failed

Increase:

```nginx
client_max_body_size 10M;
```

## Related Documentation

- [Nginx Troubleshooting](https://github.com/Yukitojp/RustChat/blob/main/docs/nginx-troubleshooting.md)
- [Deployment Overview](overview.md)
