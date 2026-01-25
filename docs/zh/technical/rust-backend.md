# Rust 后端

RushChat 的后端使用 Rust 编写，基于 Axum 框架。

## Rust 后端概览

```markmap
# Rust 后端
## 技术栈
- Rust
  - 系统编程语言
  - 高性能
  - 内存安全
- Axum
  - 异步Web框架
  - 路由系统
  - 中间件
- Tokio
  - 异步运行时
  - 任务调度
- SQLx
  - 类型安全SQL
  - MySQL驱动
  - 异步查询
- Serde
  - 序列化/反序列化
  - JSON处理
- Bcrypt
  - 密码加密
  - 安全存储
## 项目结构
- models/
  - user.rs
  - message.rs
  - channel.rs
  - 数据模型
- handlers/
  - auth.rs
  - user.rs
  - channel.rs
  - HTTP处理器
- websocket/
  - connection.rs
  - events.rs
  - state.rs
  - 实时通信
- utils/
  - rpc.rs
  - permissions.rs
  - 工具函数
## 核心功能
- WebSocket通信
  - 实时消息
  - 广播机制
  - 连接管理
- REST API
  - 用户认证
  - 资源管理
  - 文件上传
- 数据库操作
  - 类型安全
  - 连接池
  - 事务支持
```

## 技术栈

- **Rust** - 系统编程语言
- **Axum** - 现代化的异步 Web 框架
- **Tokio** - 异步运行时
- **SQLx** - 类型安全的异步 SQL 工具包（MySQL）
- **Serde** - 序列化/反序列化
- **Bcrypt** - 密码加密

## 项目结构

```
server-rust/
├── src/
│   ├── main.rs              # 入口文件
│   ├── config.rs            # 配置管理
│   ├── db.rs                # 数据库连接
│   ├── models/              # 数据模型
│   │   ├── user.rs
│   │   ├── message.rs
│   │   ├── channel.rs
│   │   └── ...
│   ├── handlers/            # HTTP 处理器
│   │   ├── auth.rs
│   │   ├── user.rs
│   │   ├── channel.rs
│   │   └── ...
│   ├── websocket/           # WebSocket 处理器
│   │   ├── connection.rs
│   │   ├── events.rs
│   │   └── state.rs
│   └── utils/               # 工具函数
│       ├── rpc.rs           # RPC 工具（NFT 验证等）
│       └── permissions.rs
├── Cargo.toml
└── README.md
```

## 核心功能

### WebSocket 实时通信

- 基于 Tokio WebSocket
- 支持广播消息
- 连接管理和心跳检测

### RESTful API

- 用户认证
- 用户管理
- 频道管理
- 消息管理
- 文件上传

### 数据库集成

- 使用 SQLx 进行类型安全的查询
- 连接池管理
- 异步数据库操作

### 文件上传

- 头像上传
- 表情包上传
- 图片压缩

## 开发

### 运行开发服务器

```bash
cd server-rust
cargo run
```

### 编译生产版本

```bash
cargo build --release
```

### 运行测试

```bash
cargo test
```

## 性能优化

- 使用连接池管理数据库连接
- 异步 I/O 处理
- 广播通道用于 WebSocket 消息分发
- 类型安全的数据库查询

## 相关文档

- [架构设计](architecture.md)
- [API 文档](api.md)
- [数据库设计](database.md)
