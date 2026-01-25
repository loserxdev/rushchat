# React 前端

RushChat 的前端使用 React 18 构建。

## 技术栈

- **React 18** - UI 框架
- **Socket.io Client** - WebSocket 通信
- **CSS Variables** - 主题系统
- **React Context** - 状态管理
- **Wagmi** - Ethereum 钱包连接
- **Viem** - Ethereum 工具库

## 项目结构

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
│   │   ├── index.js
│   │   └── locales/
│   │       ├── zh.js
│   │       └── en.js
│   └── config/              # 配置文件
│       └── wagmi.js
├── public/                  # 静态文件
└── package.json
```

## 核心组件

### ChatRoom

主聊天室组件，包含：

- 消息列表
- 消息输入
- 用户列表
- 表情选择器

### ChannelManager

频道管理组件，包含：

- 频道列表
- 频道创建
- 频道切换

### WalletConnect

钱包连接组件，支持：

- MetaMask
- OKX Wallet
- Phantom
- Coinbase Wallet
- 其他 EVM 和 Solana 钱包

## 功能特性

### 实时通信

- WebSocket 连接
- 自动重连
- 消息实时更新

### 主题系统

- 日夜间模式
- CSS Variables
- 平滑过渡动画

### 国际化

- 支持中文和英文
- 使用 i18next
- 动态语言切换

### 响应式设计

- 移动端适配
- 桌面端优化
- 自适应布局

## 开发

### 安装依赖

```bash
cd client
npm install
```

### 启动开发服务器

```bash
npm start
```

### 构建生产版本

```bash
npm run build
```

## 相关文档

- [架构设计](architecture.md)
- [API 文档](api.md)
