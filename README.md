# RushChat 文档

> 基于 Rust 后端和 React 前端构建的实时聊天应用

![RushChat](https://img.shields.io/badge/RushChat-v2.0.0-blue)
![Rust](https://img.shields.io/badge/Rust-1.70+-orange)
![React](https://img.shields.io/badge/React-18-blue)

## 🚀 简介

RushChat 是一个现代化的实时聊天应用，采用 Rust 后端和 React 前端构建，支持多频道、实时消息、表情包、合约推荐等功能。

## ✨ 核心特性

- 💬 **实时通信** - 基于 WebSocket 的即时消息传递
- 📱 **多频道支持** - 公共频道和私密频道
- 👥 **用户系统** - 游客模式、注册登录、个人资料管理
- 🔐 **权限管理** - 三级管理员体系
- 💰 **积分系统** - 用户积分管理和频道创建消耗
- 🏆 **荣誉等级** - 0-10级荣誉体系
- 🎁 **邀请系统** - 个性化邀请码、分享到X、二维码分享
- 📊 **合约推荐** - 用户推荐合约，支持多表情投票
- 😊 **表情包系统** - 系统表情 + 用户自定义 GIF 表情包
- 🎤 **语音聊天** - 私有频道支持 WebRTC 语音通话（规划中）

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
- [安装指南](installation.md) - 如何安装和配置 RushChat
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
