# MkDocs 部署故障排除

## "Content owner not found" 错误

### 问题描述

在部署 MkDocs 文档站点时遇到 "Content owner not found" 错误。

### 可能原因和解决方案

#### 1. Vercel 部署错误

**症状**：在 Vercel 部署时出现 "Content owner not found"

**可能原因**：
- Vercel 项目配置错误
- 缺少或错误的 Vercel token
- 项目权限问题

**解决方案**：

1. **检查 Vercel 项目配置**
   - 登录 Vercel 控制台
   - 检查项目设置中的 Root Directory 是否正确
   - 对于 MkDocs，Root Directory 应设置为 `gitbook`

2. **检查环境变量**
   - 确保 `VERCEL_PROJECT_ID`、`VERCEL_ORG_ID`、`VERCEL_TOKEN` 正确配置
   - 如果使用 GitHub Actions，确保这些变量已添加到仓库 Secrets

3. **重新连接项目**
   - 在 Vercel 中删除并重新导入项目
   - 确保有正确的仓库访问权限

#### 2. GitHub Pages 部署错误

**症状**：在 GitHub Pages 部署时出现 "Content owner not found"

**可能原因**：
- 仓库权限问题
- GitHub Actions 配置错误
- 部署分支设置错误

**解决方案**：

1. **检查仓库权限**
   - 确保 GitHub Actions 有写入权限
   - 在仓库 Settings → Actions → General 中启用 "Read and write permissions"

2. **检查部署配置**
   ```yaml
   # .github/workflows/deploy.yml
   permissions:
     contents: write
   ```

3. **检查部署分支**
   - 确保部署分支（通常是 `gh-pages`）存在
   - 检查 GitHub Pages 设置中的 Source 分支

#### 3. 手动部署到 Vercel

如果使用 Vercel CLI 手动部署：

```bash
# 安装 Vercel CLI
npm i -g vercel

# 登录
vercel login

# 在 gitbook 目录中部署
cd gitbook
vercel --prod
```

#### 4. 使用 GitHub Actions 部署到 GitHub Pages

创建 `.github/workflows/deploy-docs.yml`：

```yaml
name: Deploy Docs

on:
  push:
    branches:
      - main
    paths:
      - 'gitbook/**'

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.x'
      
      - name: Install dependencies
        run: |
          pip install mkdocs mkdocs-material mkdocs-static-i18n mkdocs-markmap
      
      - name: Build docs
        working-directory: gitbook
        run: mkdocs build
      
      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./gitbook/site
          cname: your-domain.com  # 如果有自定义域名
```

### 验证步骤

1. **本地构建测试**
   ```bash
   cd gitbook
   mkdocs build
   ```
   如果本地构建成功，问题可能在部署配置

2. **检查生成的文件**
   ```bash
   ls -la gitbook/site/
   ```
   确保 `site/` 目录包含所有必要的文件

3. **检查部署日志**
   - Vercel: 查看 Deployment Logs
   - GitHub Pages: 查看 Actions 日志

### 常见配置问题

#### MkDocs 配置检查清单

- [ ] `site_url` 正确设置（包含子目录路径，如果适用）
- [ ] `docs_dir` 和 `site_dir` 路径正确
- [ ] 所有插件正确安装
- [ ] `mkdocs.yml` 语法正确

#### 部署平台配置检查清单

**Vercel**:
- [ ] Root Directory 设置为 `gitbook`
- [ ] Build Command: `mkdocs build`
- [ ] Output Directory: `site`
- [ ] Framework: Other

**GitHub Pages**:
- [ ] 启用 GitHub Actions
- [ ] 设置正确的 Source 分支
- [ ] 检查仓库权限设置

### 获取更多帮助

如果问题仍然存在：

1. 检查部署平台的官方文档
2. 查看部署日志中的详细错误信息
3. 确认 MkDocs 和插件版本兼容性
