# GitBook 替代方案

由于 GitBook CLI 与 Node.js 20 不兼容，这里提供几种替代方案。

## 方案 1: 使用 GitBook.com（推荐）

最简单的方法，无需本地安装。

### 步骤

1. **注册 GitBook 账号**
   - 访问 https://www.gitbook.com/
   - 使用 GitHub 账号登录

2. **创建新空间（Space）**
   - 点击 "Create a new space"
   - 选择 "Import from GitHub"
   - 选择 RushChat 仓库
   - 设置路径为 `gitbook/`

3. **自动发布**
   - GitBook 会自动识别 `SUMMARY.md`
   - 自动生成文档网站
   - 可以自定义域名

### 优点
- ✅ 无需本地安装
- ✅ 自动更新（连接 GitHub）
- ✅ 免费托管
- ✅ 支持自定义域名

## 方案 2: 使用 MkDocs（Python）

现代化的文档工具，支持 Markdown。

### 安装

```bash
pip install mkdocs mkdocs-material
```

### 使用

```bash
cd gitbook
mkdocs serve
```

访问：http://127.0.0.1:8000

### 创建 mkdocs.yml

```yaml
site_name: RushChat 文档
site_description: 基于 Rust 后端和 React 前端构建的实时聊天应用

theme:
  name: material
  language: zh

nav:
  - 介绍: README.md
  - 快速开始: getting-started.md
  - 安装指南: installation.md
  - 配置说明: configuration.md
  - 用户指南:
    - 用户系统: user-guide/user-system.md
  - 技术文档:
    - 架构设计: technical/architecture.md
    - 数据库设计: technical/database.md
  - 更新日志: changelog.md
  - 常见问题: faq.md
```

## 方案 3: 使用 VitePress（Vue）

Vite 驱动的静态站点生成器，速度快。

### 安装

```bash
npm install -D vitepress
```

### 使用

```bash
cd gitbook
npx vitepress dev
```

## 方案 4: 使用 Docusaurus（React）

Facebook 的文档工具，功能强大。

### 安装

```bash
npx create-docusaurus@latest docs classic
```

### 优点
- ✅ 功能丰富
- ✅ 支持搜索
- ✅ 支持多语言
- ✅ 支持版本控制

## 方案 5: 使用 Node.js 降级（不推荐）

如果必须使用 GitBook CLI，可以降级 Node.js：

```bash
# 使用 nvm 安装 Node.js 16
nvm install 16
nvm use 16

# 然后安装 GitBook
npm install -g gitbook-cli
gitbook install
```

**注意**：不推荐此方法，因为会限制其他项目的 Node.js 版本。

## 推荐方案

**最佳选择：GitBook.com**
- 最简单
- 无需配置
- 自动更新
- 免费托管

**开发环境：MkDocs**
- 本地预览方便
- 支持热重载
- 配置简单

## 快速开始（GitBook.com）

1. 访问 https://www.gitbook.com/
2. 使用 GitHub 登录
3. 创建新空间
4. 连接 GitHub 仓库
5. 设置路径：`gitbook/`
6. 完成！

文档会自动发布到 `https://your-space.gitbook.io/rushchat/`
