# 配置说明

RushChat 的配置主要通过环境变量进行。

## 环境变量

### 后端配置

在项目根目录创建 `.env` 文件（后端会优先加载项目根目录的 `.env`）。

#### 基础服务

```env
PORT=5001                    # 后端服务端口
NODE_ENV=development         # 环境模式：development | production
CLIENT_URL=http://localhost:3000  # 前端地址（用于 CORS）
MAIN_DOMAIN=localhost        # 主域名（生产环境设置为实际域名）
```

#### 数据库

```env
DB_HOST=localhost            # 数据库主机
DB_PORT=3306                 # 数据库端口
DB_USER=root                 # 数据库用户名
DB_PASSWORD=your_password    # 数据库密码
DB_NAME=rushchat             # 数据库名称
```

#### Solana RPC（可选）

```env
SOL_HTTP_RPC=https://api.mainnet-beta.solana.com
SOL_RPC=https://api.mainnet-beta.solana.com
SOL_MAINNET_RPC=https://rozanna-srqsog-fast-mainnet.helius-rpc.com
```

#### 红包合约（可选）

```env
# EVM 链红包合约地址
RED_PACKET_CONTRACT_ADDRESS=

# Solana 红包程序 ProgramId（Base58，通常 32~44 长度）
# 重要：必须是"程序 ProgramId"，不是钱包地址
SOLANA_RED_PACKET_PROGRAM_ID=
```

### 前端配置

在 `client/` 目录创建 `.env` 文件：

```env
REACT_APP_API_URL=http://localhost:5001
REACT_APP_SOCKET_URL=http://localhost:5001
```

## 配置文件

### 数据库配置

数据库配置通过环境变量读取，无需额外配置文件。

### 频道规则配置

频道规则存储在数据库中，通过管理界面或 API 进行配置。

## 生产环境配置

### Railway 部署

在 Railway 项目设置中配置环境变量：

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

### Vercel 部署

在 Vercel 项目设置中配置环境变量：

```env
REACT_APP_API_URL=https://your-backend.railway.app
REACT_APP_SOCKET_URL=https://your-backend.railway.app
```

## 安全配置

### CORS 配置

后端通过 `CLIENT_URL` 环境变量控制 CORS 允许的来源。

### 数据库安全

- 使用强密码
- 限制数据库访问 IP
- 定期备份数据库

### 生产环境建议

- 使用 HTTPS
- 设置强密码策略
- 启用数据库 SSL 连接
- 配置防火墙规则

## 环境变量优先级

后端环境变量加载顺序：

1. 项目根目录 `.env` 文件
2. 系统环境变量
3. 默认值

## 配置验证

### 检查环境变量

```bash
# 后端
cd server-rust
cargo run -- --check-env

# 前端
cd client
npm run check-env
```

### 测试数据库连接

```bash
mysql -u $DB_USER -p$DB_PASSWORD -h $DB_HOST -P $DB_PORT $DB_NAME -e "SELECT 1;"
```

## 常见配置问题

### CORS 错误

确保 `CLIENT_URL` 包含协议（`http://` 或 `https://`）

### 数据库连接失败

检查数据库凭据和网络连接

### 端口冲突

更改 `PORT` 环境变量，并更新前端 `REACT_APP_SOCKET_URL`

## 参考

- [环境变量模板](../docs/ENVIRONMENT_TEMPLATE.md)
- [部署指南](deployment/overview.md)
