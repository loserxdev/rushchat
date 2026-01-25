# GitBook 文档说明

本目录包含 RushChat 项目的 GitBook 格式文档。

## 文档结构

```
gitbook/
├── README.md              # 首页
├── SUMMARY.md             # 目录文件（GitBook 必需）
├── getting-started.md     # 快速开始
├── installation.md        # 安装指南
├── configuration.md       # 配置说明
├── changelog.md          # 更新日志
├── faq.md                # 常见问题
├── user-guide/           # 用户指南
│   └── user-system.md
├── admin-guide/          # 管理员指南
├── features/             # 功能特性
├── technical/            # 技术文档
│   ├── architecture.md
│   └── database.md
├── deployment/           # 部署指南
└── development/          # 开发指南
```

## 如何使用

### 方法 1: 使用 GitBook CLI

```bash
# 安装 GitBook CLI
npm install -g gitbook-cli

# 安装 GitBook
gitbook install

# 启动本地服务器
cd gitbook
gitbook serve

# 访问 http://localhost:4000
```

### 方法 2: 使用 GitBook.com

1. 注册 GitBook 账号
2. 创建新空间（Space）
3. 连接 GitHub 仓库
4. 选择 `gitbook/` 目录作为文档根目录
5. GitBook 会自动识别 `SUMMARY.md` 并生成文档

### 方法 3: 使用其他文档工具

这些 Markdown 文件也可以用于：
- **MkDocs** - Python 文档生成工具
- **Docusaurus** - Facebook 的文档工具
- **VitePress** - Vite 驱动的静态站点生成器
- **VuePress** - Vue 驱动的静态站点生成器

## 文档维护

### 添加新章节

1. 在相应目录创建 `.md` 文件
2. 在 `SUMMARY.md` 中添加链接

### 更新文档

1. 编辑相应的 `.md` 文件
2. 提交到 Git 仓库
3. GitBook 会自动更新（如果已连接）

## 文档来源

本文档从以下现有文档提取和整理：

- `README.md` - 项目主 README
- `DOCUMENTATION.md` - 完整文档
- `docs/` - 文档目录
- `database/README.md` - 数据库文档
- `server-rust/README.md` - Rust 后端文档

## 下一步

- 完善各章节内容
- 添加更多示例和截图
- 添加 API 文档
- 添加部署指南详细步骤

## 相关链接

- [GitBook 官网](https://www.gitbook.com/)
- [GitBook 文档](https://docs.gitbook.com/)
- [Markdown 语法](https://www.markdownguide.org/)
