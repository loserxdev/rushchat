# Vercel 部署

使用 Vercel 部署 RushChat 前端应用。

## 前置要求

- Vercel 账号（https://vercel.com/）
- GitHub 账号
- 已推送代码到 GitHub

## 部署步骤

### 1. 创建 Vercel 项目

1. 登录 Vercel
2. 点击 "Add New Project"
3. 选择 RushChat 仓库
4. 配置项目设置：
   - **Framework Preset**: Create React App
   - **Root Directory**: `client`
   - **Build Command**: `npm run build`
   - **Output Directory**: `build`

### 2. 配置环境变量

在项目设置中添加环境变量：

```env
REACT_APP_API_URL=https://your-backend.railway.app
REACT_APP_SOCKET_URL=https://your-backend.railway.app
```

### 3. 部署

1. 点击 "Deploy"
2. Vercel 会自动构建和部署
3. 等待部署完成
4. 获得部署 URL

### 4. 配置自定义域名

1. 在项目设置中
2. 点击 "Domains"
3. 添加自定义域名
4. 配置 DNS 记录

## 自动部署

### GitHub 集成

Vercel 会自动：

- 监听 GitHub 推送
- 自动触发部署
- 生成预览部署（Pull Request）

### 预览部署

每个 Pull Request 都会生成预览部署：

- 独立的部署 URL
- 用于测试和预览
- 不影响生产环境

## 构建优化

### 环境变量

确保所有环境变量都已配置：

- `REACT_APP_API_URL`
- `REACT_APP_SOCKET_URL`
- 其他前端需要的变量

### 构建配置

Vercel 会自动优化：

- 代码分割
- 资源压缩
- CDN 分发

## 故障排除

### 构建失败

- 检查 Node.js 版本
- 检查依赖是否正确
- 查看构建日志

### 运行时错误

- 检查环境变量
- 检查 API URL 配置
- 查看浏览器控制台

### CORS 错误

- 检查后端 CORS 配置
- 确保 `CLIENT_URL` 正确
- 检查域名是否匹配

## 相关文档

- [部署概述](overview.md)
- [环境变量](environment.md)
