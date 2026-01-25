# 部署概述

RushChat 的部署方案总览。

## 部署方案概览

```markmap
# 部署方案
## 后端部署
- Railway
  - 推荐方案
  - 简单易用
  - 自动部署
- Fly.io
  - 支持Rust
  - 性能好
- Hetzner
  - 自托管
  - 性价比高
- 云服务商
  - AWS
  - GCP
  - Azure
## 前端部署
- Vercel
  - 推荐方案
  - 自动部署
  - 全球CDN
- Netlify
  - 类似Vercel
  - 静态托管
- Cloudflare Pages
  - 全球CDN
  - 快速访问
- GitHub Pages
  - 免费托管
  - 静态站点
## 数据库
- Railway MySQL
  - 与后端一起
  - 简单配置
- PlanetScale
  - 无服务器
  - 自动扩展
- Supabase
  - PostgreSQL
  - 需要迁移
- 自托管MySQL
  - 完全控制
  - 需要维护
## 部署架构
- 前端层
  - Vercel
  - React App
- 后端层
  - Railway
  - Rust Server
- 数据层
  - Railway MySQL
  - 数据持久化
```

## 推荐部署方案

### 后端部署

- **Railway** - 推荐，简单易用
- **Fly.io** - 支持 Rust，性能好
- **Hetzner** - 自托管，性价比高
- **AWS/GCP/Azure** - 企业级，功能丰富

### 前端部署

- **Vercel** - 推荐，自动部署
- **Netlify** - 类似 Vercel
- **Cloudflare Pages** - 全球 CDN
- **GitHub Pages** - 免费静态托管

### 数据库

- **Railway MySQL** - 与后端一起部署
- **PlanetScale** - 无服务器 MySQL
- **Supabase** - PostgreSQL（需要迁移）
- **自托管 MySQL** - 完全控制

## 部署架构

```
┌─────────────────┐
│  Vercel (前端)   │
│  React App      │
└────────┬────────┘
         │ HTTPS
         │
┌────────▼────────┐
│  Railway (后端) │
│  Rust Server    │
└────────┬────────┘
         │
┌────────▼────────┐
│  Railway MySQL  │
│  数据库         │
└─────────────────┘
```

## 部署步骤

### 1. 准备环境

- 确保代码已推送到 GitHub
- 准备环境变量
- 准备数据库

### 2. 部署后端

- 创建 Railway 项目
- 配置环境变量
- 部署 Rust 服务

### 3. 部署前端

- 创建 Vercel 项目
- 配置环境变量
- 部署 React 应用

### 4. 配置域名

- 配置后端域名
- 配置前端域名
- 更新 CORS 设置

## 环境变量

### 后端环境变量

```env
DB_HOST=...
DB_PORT=3306
DB_USER=...
DB_PASSWORD=...
DB_NAME=rushchat
PORT=5001
NODE_ENV=production
CLIENT_URL=https://your-frontend.vercel.app
MAIN_DOMAIN=your-domain.com
```

### 前端环境变量

```env
REACT_APP_API_URL=https://your-backend.railway.app
REACT_APP_SOCKET_URL=https://your-backend.railway.app
```

## 相关文档

- [Railway 部署](railway.md)
- [Vercel 部署](vercel.md)
- [环境变量](environment.md)
- [Nginx 配置](nginx.md)
