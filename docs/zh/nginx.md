# Nginx 配置

使用 Nginx 作为反向代理的配置说明。

## 基本配置

### HTTP 到 HTTPS 重定向

```nginx
server {
    listen 80;
    server_name your-domain.com;
    return 301 https://$server_name$request_uri;
}
```

### HTTPS 配置

```nginx
server {
    listen 443 ssl http2;
    server_name your-domain.com;

    ssl_certificate /path/to/cert.pem;
    ssl_certificate_key /path/to/key.pem;

    # SSL 配置
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;
    ssl_prefer_server_ciphers on;

    # 代理到后端
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

    # WebSocket 支持
    location /ws {
        proxy_pass http://localhost:5001;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        
        # WebSocket 超时设置
        proxy_read_timeout 86400;
    }

    # 静态文件（前端）
    location / {
        root /path/to/client/build;
        try_files $uri $uri/ /index.html;
    }

    # 文件上传
    client_max_body_size 10M;
}
```

## 完整配置示例

参考 `docs/nginx-config-example.conf` 获取完整配置。

## 故障排除

### 301 重定向循环

检查：

- SSL 证书配置
- 代理设置
- 域名配置

### WebSocket 连接失败

确保：

- 正确配置 `Upgrade` 和 `Connection` headers
- 设置足够的超时时间
- 检查防火墙规则

### 文件上传失败

增加：

```nginx
client_max_body_size 10M;
```

## 相关文档

- [Nginx 故障排除](https://github.com/Yukitojp/RustChat/blob/main/docs/nginx-troubleshooting.md)
- [部署概述](overview.md)
