# Rush.Moe 文档

> Solana 原生 Web3 实时聊天应用（兼容 EVM）

![Rush.Moe](https://img.shields.io/badge/Rush.Moe-v2.0.0-blue)
![Rust](https://img.shields.io/badge/Rust-1.70+-orange)
![React](https://img.shields.io/badge/React-18-blue)

## 🚀 简介

**Rush.Moe** 是 Solana 原生 Web3 实时聊天应用（同时兼容 EVM）。**第一时间发现 Alpha 即时交易**是 Rush 的核心理念。

任何人可以在 Rush.Moe 构建自己的 Alpha 频道（可选择付费、私有，同时赚取交易手续费，支持 Solana & EVM NFT 验证进入私有频道）。语音聊天更能提升社区的即时交流效率。

邀请朋友加入 Rush.Moe，分享建立频道手续费 & 交易手续费（后续功能）。

## ✨ 核心特性

```markmap
# Rush.Moe 核心特性
## 通信功能
- 实时消息
  - WebSocket
  - 文本消息
  - 图片分享
- 语音聊天
  - WebRTC
  - 屏幕共享
  - 多人支持
  - 提升社区效率
## Alpha 频道系统
- 构建自己的 Alpha 频道
  - 付费频道
  - 私有频道
  - 赚取交易手续费
- 频道访问控制
  - Solana NFT 验证
  - EVM NFT 验证
  - 密码保护
## 用户管理
- 游客模式
- 注册登录
- 个人资料
  - 头像
  - 钱包地址
  - 邮箱
## 权限系统
- 三级管理员
  - A级（超级管理员）
  - B级（Rush高管）
  - C级（普通管理员）
## 积分荣誉
- 积分系统
  - 频道创建
  - 邀请奖励
- 荣誉等级（0-10级）
## 社交功能
- 邀请系统
  - 分享建立频道手续费
  - 分享交易手续费（后续功能）
- 合约推荐
- 表情包系统
  - 系统表情
  - 自定义GIF表情
## 区块链集成
- Solana 原生支持
- EVM 兼容
- 钱包验证
  - EVM钱包
  - Solana钱包
- 红包系统
  - EVM链
  - Solana链
- X402协议
```

## 🎯 核心理念

**第一时间发现 Alpha 即时交易**是 Rush 的核心理念。

Rush.Moe 让用户可以：
- 构建和管理 Alpha 频道
- 通过频道创建和交易手续费赚取收益
- 通过 NFT 验证访问专属私有频道
- 通过语音聊天实现即时交流

## 🌟 主要功能

### Alpha 频道系统

- ✅ **构建自己的 Alpha 频道** - 创建付费或私有频道
- ✅ **赚取交易手续费** - 从频道活动中获得收益
- ✅ **NFT 验证** - Solana & EVM NFT 验证进入私有频道
- ✅ **灵活的访问控制** - 密码保护和钱包验证

### 实时通信

- 💬 **实时消息** - 基于 WebSocket 的即时消息传递
- 🎤 **语音聊天** - 私有频道支持 WebRTC 语音通话，支持屏幕共享
- 📱 **多频道支持** - 公共频道和私有频道

### Web3 集成

- 🔗 **Solana 原生** - 为 Solana 生态系统构建
- ⛓️ **EVM 兼容** - 支持以太坊、BSC、Polygon 等
- 🔐 **钱包验证** - 连接 EVM 和 Solana 钱包
- 💰 **收益分享** - 分享建立频道手续费 & 交易手续费（后续功能）

### 社交功能

- 👥 **用户系统** - 游客模式、注册登录、个人资料管理
- 🎁 **邀请系统** - 个性化邀请码、分享到X、二维码分享
- 📊 **合约推荐** - 用户推荐合约，支持多表情投票
- 😊 **表情包系统** - 系统表情 + 用户自定义 GIF 表情包

## 🛠️ 技术栈

### 后端
- **Rust** - 系统编程语言
- **Axum** - 异步 Web 框架
- **Tokio** - 异步运行时
- **SQLx** - 类型安全的异步 SQL 工具包（MySQL）

### 前端
- **React 18** - UI 框架
- **Socket.io Client** - WebSocket 通信
- **CSS3** - 现代化样式

### 数据库
- **MySQL 5.7+** - 关系型数据库

## 📚 文档导航

### 快速开始
- [安装指南](installation.md) - 如何安装和配置 Rush.Moe
- [快速开始](getting-started.md) - 5分钟快速上手
- [配置说明](configuration.md) - 环境变量和配置文件

### 用户指南
- [用户系统](user-guide/user-system.md) - 注册、登录、游客模式
- [实时聊天](user-guide/chat.md) - 发送消息、图片、表情
- [频道系统](user-guide/channels.md) - 创建和加入频道
- [表情包系统](user-guide/stickers.md) - 使用和管理表情包

### 管理员指南
- [管理员系统](admin-guide/admin-system.md) - 三级管理员体系
- [管理操作](admin-guide/operations.md) - 踢人、禁言、任命

### 技术文档
- [架构设计](technical/architecture.md) - 系统架构和技术选型
- [API 文档](technical/api.md) - RESTful API 接口说明
- [WebSocket 事件](technical/websocket.md) - WebSocket 事件列表

### 部署指南
- [部署概述](deployment/overview.md) - 部署方案总览
- [Railway 部署](deployment/railway.md) - 后端部署到 Railway
- [Vercel 部署](deployment/vercel.md) - 前端部署到 Vercel

## 🎯 快速开始

```bash
# 1. 克隆项目
git clone <repository-url>
cd RushChat

# 2. 安装依赖
npm install
cd client && npm install && cd ..

# 3. 创建数据库
mysql -u root -p < database/schema.sql

# 4. 配置环境变量
cp docs/ENVIRONMENT_TEMPLATE.md .env

# 5. 启动应用
cd server-rust && cargo run
cd ../client && npm start
```

访问：`http://localhost:3000`

## 📖 更多信息

- [更新日志](changelog.md) - 版本更新记录
- [常见问题](faq.md) - 常见问题解答
- [故障排除](troubleshooting.md) - 问题排查指南

## 📄 许可证

MIT License - 欢迎用于学习和开发。

---

**使用 Rust、React 和 MySQL 构建 ❤️**
