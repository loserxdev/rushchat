# 快速开始 - 本地预览文档

由于 GitBook CLI 与 Node.js 20 不兼容，这里提供两种快速预览文档的方法。

## 方法 1: 使用 MkDocs（推荐，简单快速）

### 安装

```bash
# 使用 pip 安装
pip install mkdocs mkdocs-material

# 或使用 pip3
pip3 install mkdocs mkdocs-material
```

### 启动

```bash
cd gitbook
mkdocs serve
```

访问：**http://127.0.0.1:8000**

### 构建静态网站

```bash
mkdocs build
```

生成的文件在 `site/` 目录，可以部署到任何静态网站托管服务。

## 方法 2: 使用 GitBook.com（在线，无需安装）

### 步骤

1. 访问 https://www.gitbook.com/
2. 使用 GitHub 账号登录
3. 点击 "Create a new space"
4. 选择 "Import from GitHub"
5. 选择 RushChat 仓库
6. 设置路径为 `gitbook/`
7. 完成！

文档会自动发布，可以自定义域名。

## 方法 3: 使用 VitePress（Vue，现代化）

### 安装

```bash
npm install -D vitepress
```

### 启动

```bash
cd gitbook
npx vitepress dev
```

访问：**http://localhost:5173**

## 方法 4: 使用 Docusaurus（React，功能强大）

### 安装

```bash
npx create-docusaurus@latest docs classic --typescript
```

### 配置

将 `gitbook/` 目录的内容复制到 `docs/docs/`，然后：

```bash
cd docs
npm start
```

## 推荐方案对比

| 方案 | 难度 | 速度 | 功能 | 推荐度 |
|------|------|------|------|--------|
| **MkDocs** | ⭐ 简单 | ⭐⭐⭐ 快 | ⭐⭐⭐ 丰富 | ⭐⭐⭐⭐⭐ |
| **GitBook.com** | ⭐ 最简单 | ⭐⭐⭐ 快 | ⭐⭐⭐⭐ 非常丰富 | ⭐⭐⭐⭐⭐ |
| **VitePress** | ⭐⭐ 中等 | ⭐⭐⭐⭐ 很快 | ⭐⭐⭐ 中等 | ⭐⭐⭐⭐ |
| **Docusaurus** | ⭐⭐⭐ 复杂 | ⭐⭐ 中等 | ⭐⭐⭐⭐⭐ 最丰富 | ⭐⭐⭐ |

## 快速命令参考

### MkDocs

```bash
# 安装
pip install mkdocs mkdocs-material

# 启动开发服务器
cd gitbook && mkdocs serve

# 构建静态网站
mkdocs build

# 部署到 GitHub Pages
mkdocs gh-deploy
```

### GitBook.com

1. 登录 https://www.gitbook.com/
2. 导入 GitHub 仓库
3. 设置路径：`gitbook/`
4. 完成！

## 故障排除

### MkDocs 安装失败

```bash
# 使用 pip3
pip3 install mkdocs mkdocs-material

# 或使用 --user
pip install --user mkdocs mkdocs-material
```

### 端口被占用

```bash
# MkDocs 使用其他端口
mkdocs serve -a 127.0.0.1:8001
```

## 下一步

选择一种方法开始预览文档：

1. **本地开发**：使用 MkDocs
2. **在线发布**：使用 GitBook.com
3. **高级功能**：使用 Docusaurus

所有文档文件已准备好，可以直接使用！
