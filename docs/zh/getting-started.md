# 快速开始

本指南将帮助您在 5 分钟内启动 RushChat。

## 快速开始概览

```markmap
# 快速开始指南
## 前置要求
- Node.js ≥ 18
- Rust ≥ 1.70
- MySQL ≥ 5.7
- Git
## 安装步骤
- 克隆项目
  - git clone
  - 进入目录
- 安装依赖
  - npm install
  - cd client && npm install
- 数据库设置
  - 创建数据库
  - 导入schema
- 配置环境
  - 创建.env文件
  - 设置数据库连接
  - 配置端口和URL
- 启动应用
  - 启动后端
  - 启动前端
## 启动服务
- 后端服务
  - cd server-rust
  - cargo run
  - 端口5001
- 前端服务
  - cd client
  - npm start
  - 端口3000
## 验证安装
- 检查后端
  - 健康检查端点
  - 端口监听
- 检查前端
  - 页面加载
  - 聊天界面
  - 游客模式
## 下一步
- 阅读用户指南
- 查看配置说明
- 部署到生产环境
```

## 前置要求

- **Node.js** ≥ 18
- **Rust** ≥ 1.70
- **MySQL** ≥ 5.7 或 **MariaDB** ≥ 10.3
- **Git**

## 安装步骤

### 1. 克隆项目

```bash
git clone <repository-url>
cd RushChat
```

### 2. 安装依赖

```bash
# 安装根目录依赖
npm install

# 安装客户端依赖
cd client && npm install && cd ..
```

### 3. 数据库设置

#### 创建数据库

```bash
mysql -u root -p < database/schema.sql
```

或手动执行：

```sql
mysql -u root -p
source database/schema.sql
```

#### 配置数据库连接

在项目根目录创建 `.env` 文件：

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

> 💡 提示：可以复制 `docs/ENVIRONMENT_TEMPLATE.md` 作为模板

### 4. 启动应用

#### 启动后端（Rust）

```bash
cd server-rust
cargo run
```

后端服务器将运行在：`http://localhost:5001`

#### 启动前端（React）

打开新的终端窗口：

```bash
cd client
npm start
```

React 开发服务器将运行在：`http://localhost:3000`

### 5. 访问应用

打开浏览器访问：`http://localhost:3000`

## 验证安装

### 检查后端

访问 `http://localhost:5001/api/health`（如果配置了健康检查端点）

### 检查前端

- 页面正常加载
- 可以看到聊天界面
- 可以以游客身份进入

## 下一步

- 📖 阅读 [用户指南](user-guide/user-system.md) 了解如何使用
- 🔧 查看 [配置说明](configuration.md) 进行详细配置
- 🚀 查看 [部署指南](deployment/overview.md) 部署到生产环境

## 常见问题

### 数据库连接失败

- 确保 MySQL 正在运行
- 检查 `.env` 文件中的数据库凭据
- 验证数据库是否存在：`mysql -u root -p -e "SHOW DATABASES;"`

### 端口已被占用

- 在 `.env` 文件中更改 `PORT`
- 更新客户端中的 `REACT_APP_SOCKET_URL`

### CORS 错误

- 检查后端 `CLIENT_URL` 环境变量
- 确保前端地址包含协议（`http://` 或 `https://`）

## 需要帮助？

- 📖 查看 [常见问题](faq.md)
- 🔍 查看 [故障排除](troubleshooting.md)
- 📝 查看 [完整文档](README.md)
