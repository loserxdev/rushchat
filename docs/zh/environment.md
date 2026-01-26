# 环境变量

RushChat 的环境变量配置说明。

## 后端环境变量

### 数据库配置

```env
DB_HOST=localhost              # 数据库主机
DB_PORT=3306                   # 数据库端口
DB_USER=root                   # 数据库用户名
DB_PASSWORD=your_password      # 数据库密码
DB_NAME=rushchat               # 数据库名称
```

### 服务器配置

```env
PORT=5001                      # 服务端口
NODE_ENV=production            # 环境模式
CLIENT_URL=https://your-app.vercel.app  # 前端地址（CORS）
MAIN_DOMAIN=your-domain.com    # 主域名
```

### Solana 配置（可选）

```env
SOL_HTTP_RPC=https://api.mainnet-beta.solana.com
SOL_RPC=https://api.mainnet-beta.solana.com
SOLANA_RED_PACKET_PROGRAM_ID=your_program_id
```

### EVM 配置（可选）

```env
RED_PACKET_CONTRACT_ADDRESS=0x...
BSC_RPC_URL=https://bsc-dataseed.binance.org/
ETH_RPC_URL=https://eth.llamarpc.com
```

## 前端环境变量

### API 配置

```env
REACT_APP_API_URL=https://your-backend.railway.app
REACT_APP_SOCKET_URL=https://your-backend.railway.app
```

## Railway 环境变量

Railway 使用模板变量引用数据库：

```env
DB_HOST=${{MySQL.MYSQLHOST}}
DB_PORT=${{MySQL.MYSQLPORT}}
DB_USER=${{MySQL.MYSQLUSER}}
DB_PASSWORD=${{MySQL.MYSQLPASSWORD}}
DB_NAME=${{MySQL.MYSQLDATABASE}}
```

## Vercel 环境变量

在 Vercel 项目设置中配置：

- 所有 `REACT_APP_*` 变量
- 区分生产、预览、开发环境

## 安全建议

### 生产环境

- 使用强密码
- 定期轮换密钥
- 限制数据库访问 IP
- 启用 SSL/TLS

### 环境变量管理

- 不要提交 `.env` 到 Git
- 使用环境变量管理工具
- 定期审查环境变量

## 相关文档

- [配置说明](../configuration.md)
- [Railway 部署](railway.md)
- [Vercel 部署](vercel.md)
