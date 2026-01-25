# 开发环境

设置 RushChat 开发环境的详细说明。

## 前置要求

### 必需软件

- **Node.js** ≥ 18
- **Rust** ≥ 1.70
- **MySQL** ≥ 5.7 或 **MariaDB** ≥ 10.3
- **Git**

### 推荐工具

- **VS Code** 或 **Cursor** - 代码编辑器
- **MySQL Workbench** - 数据库管理
- **Postman** - API 测试

## 环境设置

### 1. 安装 Node.js

```bash
# 使用 nvm（推荐）
nvm install 20
nvm use 20

# 或从官网下载
# https://nodejs.org/
```

### 2. 安装 Rust

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env
rustc --version
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

### 4. 克隆项目

```bash
git clone <repository-url>
cd RushChat
```

### 5. 安装依赖

```bash
# 根目录依赖
npm install

# 客户端依赖
cd client && npm install && cd ..
```

### 6. 数据库设置

```bash
# 创建数据库
mysql -u root -p < database/schema.sql
```

### 7. 配置环境变量

创建 `.env` 文件：

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

## 启动开发服务器

### 后端

```bash
cd server-rust
cargo run
```

### 前端

```bash
cd client
npm start
```

## 开发工具

### VS Code 扩展

推荐安装：

- Rust Analyzer
- ESLint
- Prettier
- MySQL

### 调试配置

创建 `.vscode/launch.json`：

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "lldb",
      "request": "launch",
      "name": "Debug Rust Server",
      "cargo": {
        "args": ["build", "--bin=rushchat-server"],
        "filter": {
          "name": "rushchat-server",
          "kind": "bin"
        }
      },
      "args": [],
      "cwd": "${workspaceFolder}/server-rust"
    }
  ]
}
```

## 相关文档

- [代码结构](structure.md)
- [贡献指南](contributing.md)
