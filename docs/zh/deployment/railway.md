# Railway 部署

使用 Railway 部署 RushChat 后端服务。

## Railway 部署概览

```markmap
# Railway 部署
## 前置要求
- Railway账号
- GitHub账号
- 代码已推送
## 部署步骤
- 创建项目
  - New Project
  - Deploy from GitHub
  - 选择server-rust目录
- 添加数据库
  - New → Database → MySQL
  - 自动创建
  - 记录连接信息
- 配置环境变量
  - DB_HOST
  - DB_PORT
  - DB_USER
  - DB_PASSWORD
  - DB_NAME
  - PORT
  - CLIENT_URL
- 配置构建
  - Build Command
  - Start Command
  - Root Directory
## 数据库迁移
- 运行迁移脚本
- 验证表结构
- 检查数据
## 验证部署
- 检查服务状态
- 测试API端点
- 检查日志
```

## 前置要求

- Railway 账号（https://railway.app/）
- GitHub 账号
- 已推送代码到 GitHub

## 部署步骤

### 1. 创建 Railway 项目

1. 登录 Railway
2. 点击 "New Project"
3. 选择 "Deploy from GitHub repo"
4. 选择 RushChat 仓库
5. 选择 `server-rust` 目录作为 Root Directory

### 2. 添加 MySQL 数据库

1. 在项目页面点击 "New"
2. 选择 "Database" → "MySQL"
3. Railway 会自动创建数据库
4. 记录数据库连接信息

### 3. 配置环境变量

在项目设置中添加环境变量：

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

### 4. 配置构建命令

Railway 会自动检测 Rust 项目，但可以手动配置：

**Build Command**:
```bash
cargo build --release
```

**Start Command**:
```bash
./target/release/rushchat-server
```

### 5. 运行数据库迁移

1. 在 Railway 项目页面
2. 打开 MySQL 数据库
3. 使用 Railway CLI 或 MySQL 客户端
4. 运行迁移脚本：

```bash
mysql -h $MYSQLHOST -u $MYSQLUSER -p$MYSQLPASSWORD $MYSQLDATABASE < database/schema.sql
```

### 6. 配置持久化存储

Railway 使用临时文件系统，需要配置 Volume：

1. 在项目设置中添加 Volume
2. 挂载到 `/app/uploads` 目录
3. 用于存储上传的文件

### 7. 配置域名

1. 在项目设置中
2. 点击 "Generate Domain"
3. 或添加自定义域名
4. 更新前端环境变量

## 监控和日志

### 查看日志

1. 在 Railway 项目页面
2. 点击 "Deployments"
3. 选择最新的部署
4. 查看实时日志

### 监控指标

Railway 提供：

- CPU 使用率
- 内存使用率
- 网络流量
- 请求数

## 故障排除

### 构建失败

- 检查 Rust 版本
- 检查依赖是否正确
- 查看构建日志

### 运行时错误

- 检查环境变量
- 检查数据库连接
- 查看应用日志

### 数据库连接失败

- 检查数据库服务是否运行
- 检查环境变量是否正确
- 检查网络连接

## 相关文档

- [部署概述](overview.md)
- [环境变量](environment.md)
