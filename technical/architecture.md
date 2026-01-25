# 架构设计

RushChat 的系统架构和技术选型说明。

## 系统架构

```
┌─────────────────┐
│   React 前端     │
│  (Port 3000)    │
└────────┬────────┘
         │ HTTP/WebSocket
         │
┌────────▼────────┐
│  Rust 后端      │
│  (Port 5001)    │
│  - Axum         │
│  - WebSocket    │
│  - REST API     │
└────────┬────────┘
         │
┌────────▼────────┐
│   MySQL 数据库  │
│  (Port 3306)    │
└─────────────────┘
```

## 技术栈

### 后端

- **Rust** - 系统编程语言，高性能
- **Axum** - 现代化的异步 Web 框架
- **Tokio** - 异步运行时
- **SQLx** - 类型安全的异步 SQL 工具包（MySQL）
- **Serde** - 序列化/反序列化
- **Bcrypt** - 密码加密

### 前端

- **React 18** - UI 框架
- **Socket.io Client** - WebSocket 通信
- **CSS Variables** - 主题系统
- **React Context** - 状态管理

### 数据库

- **MySQL 5.7+** - 关系型数据库
- **utf8mb4** - 字符集，支持 emoji

## 核心模块

### 后端模块

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
```

### 前端模块

```
client/
├── src/
│   ├── App.js               # 主应用组件
│   ├── index.js             # 入口文件
│   ├── components/          # React 组件
│   │   ├── ChatRoom.js
│   │   ├── ChannelManager.js
│   │   ├── MessageList.js
│   │   └── ...
│   ├── utils/               # 工具函数
│   │   ├── websocket.js
│   │   ├── wallet.js
│   │   └── ...
│   ├── i18n/                # 国际化
│   └── config/              # 配置文件
```

## 数据流

### 消息发送流程

```
用户输入消息
    ↓
前端组件处理
    ↓
WebSocket 发送 (message:send)
    ↓
后端 WebSocket 处理器
    ↓
数据库保存
    ↓
广播给所有在线用户
    ↓
前端接收并显示
```

### 用户认证流程

```
用户登录
    ↓
POST /api/auth/login
    ↓
后端验证密码
    ↓
生成会话
    ↓
返回用户信息
    ↓
前端保存会话
    ↓
WebSocket 连接
```

## 性能优化

### 后端优化

- 使用连接池管理数据库连接
- 异步 I/O 处理
- 广播通道用于 WebSocket 消息分发
- 类型安全的数据库查询

### 前端优化

- React 组件懒加载
- 消息列表虚拟滚动（规划中）
- 图片压缩和缓存
- WebSocket 自动重连

## 安全特性

- 密码加密存储（bcrypt）
- CORS 配置
- SQL 注入防护（SQLx 类型安全）
- XSS 防护（React 自动转义）
- IP 封禁机制
- 用户禁言机制

## 扩展性

### 水平扩展

- 无状态后端设计
- 数据库连接池
- WebSocket 连接管理

### 垂直扩展

- Rust 高性能
- 异步处理
- 数据库索引优化

## 相关文档

- [API 文档](api.md)
- [WebSocket 事件](websocket.md)
- [数据库设计](database.md)
