# 代码结构

RushChat 项目的代码结构说明。

## 项目结构

```
RushChat/
├── server-rust/           # Rust 后端
│   ├── src/
│   │   ├── main.rs
│   │   ├── config.rs
│   │   ├── db.rs
│   │   ├── models/       # 数据模型
│   │   ├── handlers/     # HTTP 处理器
│   │   ├── websocket/    # WebSocket 处理器
│   │   └── utils/        # 工具函数
│   └── Cargo.toml
├── client/                # React 前端
│   ├── src/
│   │   ├── components/   # React 组件
│   │   ├── utils/        # 工具函数
│   │   ├── i18n/         # 国际化
│   │   └── config/       # 配置文件
│   └── package.json
├── database/              # 数据库文件
│   ├── schema.sql
│   └── migration_*.sql
├── docs/                  # 文档
└── gitbook/              # GitBook 文档
```

## 后端结构

### models/

数据模型，包含所有数据库表的 CRUD 操作：

- `user.rs` - 用户模型
- `message.rs` - 消息模型
- `channel.rs` - 频道模型
- `ban.rs` - 封禁模型
- 等等...

### handlers/

HTTP 请求处理器：

- `auth.rs` - 认证相关
- `user.rs` - 用户相关
- `channel.rs` - 频道相关
- `message.rs` - 消息相关
- 等等...

### websocket/

WebSocket 连接和事件处理：

- `connection.rs` - 连接管理
- `events.rs` - 事件处理
- `state.rs` - 状态管理

### utils/

工具函数：

- `rpc.rs` - RPC 工具（NFT 验证等）
- `permissions.rs` - 权限检查

## 前端结构

### components/

React 组件：

- `ChatRoom.js` - 聊天室
- `ChannelManager.js` - 频道管理
- `MessageList.js` - 消息列表
- `WalletConnect.jsx` - 钱包连接
- 等等...

### utils/

工具函数：

- `websocket.js` - WebSocket 连接
- `wallet.js` - 钱包工具
- `contract.js` - 合约交互

### i18n/

国际化：

- `index.js` - i18n 配置
- `locales/zh.js` - 中文翻译
- `locales/en.js` - 英文翻译

## 代码规范

### Rust

- 使用 `rustfmt` 格式化
- 使用 `clippy` 检查
- 遵循 Rust 最佳实践

### JavaScript

- 使用 ESLint
- 使用 Prettier
- 遵循 React 最佳实践

## 相关文档

- [开发环境](setup.md)
- [贡献指南](contributing.md)
