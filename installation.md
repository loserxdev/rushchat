# 安装指南

详细的安装和配置说明。

## 系统要求

### 必需

- **Node.js** ≥ 18
- **Rust** ≥ 1.70（使用 `rustup` 安装）
- **MySQL** ≥ 5.7 或 **MariaDB** ≥ 10.3
- **Git**

### 推荐

- **npm** 或 **pnpm** 包管理器
- **cargo**（Rust 包管理器，随 Rust 安装）

## 安装步骤

### 1. 安装 Node.js

访问 [Node.js 官网](https://nodejs.org/) 下载并安装。

验证安装：

```bash
node --version  # 应显示 v18 或更高
npm --version
```

### 2. 安装 Rust

使用 `rustup` 安装：

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

验证安装：

```bash
rustc --version  # 应显示 1.70 或更高
cargo --version
```

### 3. 安装 MySQL

#### macOS

```bash
brew install mysql
brew services start mysql
```

#### Ubuntu/Debian

```bash
sudo apt-get update
sudo apt-get install mysql-server
sudo systemctl start mysql
```

#### Windows

从 [MySQL 官网](https://dev.mysql.com/downloads/mysql/) 下载安装程序。

### 4. 克隆项目

```bash
git clone <repository-url>
cd RushChat
```

### 5. 安装项目依赖

```bash
# 安装根目录依赖
npm install

# 安装客户端依赖
cd client && npm install && cd ..
```

### 6. 数据库设置

#### 创建数据库

```bash
mysql -u root -p < database/schema.sql
```

#### 运行迁移（如果数据库已存在）

```bash
mysql -u root -p rushchat < database/complete_schema_latest.sql
```

### 7. 配置环境变量

在项目根目录创建 `.env` 文件：

```env
# 基础服务
PORT=5001
NODE_ENV=development
CLIENT_URL=http://localhost:3000

# 数据库
DB_HOST=localhost
DB_PORT=3306
DB_USER=root
DB_PASSWORD=your_password
DB_NAME=rushchat

# WebSocket
REACT_APP_SOCKET_URL=http://localhost:5001

# 红包合约（可选）
RED_PACKET_CONTRACT_ADDRESS=
SOLANA_RED_PACKET_PROGRAM_ID=
```

> 💡 提示：可以复制 `docs/ENVIRONMENT_TEMPLATE.md` 作为模板

### 8. 验证安装

#### 检查数据库连接

```bash
mysql -u root -p -e "USE rushchat; SHOW TABLES;"
```

应该看到以下表：
- users
- messages
- channels
- sessions
- 等等...

#### 检查 Rust 编译

```bash
cd server-rust
cargo check
```

#### 检查前端依赖

```bash
cd client
npm list --depth=0
```

## 开发模式运行

### 启动后端

```bash
cd server-rust
cargo run
```

### 启动前端

```bash
cd client
npm start
```

## 生产模式构建

### 构建后端

```bash
cd server-rust
cargo build --release
./target/release/rushchat-server
```

### 构建前端

```bash
cd client
npm run build
```

构建产物在 `client/build/` 目录。

## 下一步

- 📖 阅读 [快速开始](getting-started.md)
- 🔧 查看 [配置说明](configuration.md)
- 🚀 查看 [部署指南](deployment/overview.md)
