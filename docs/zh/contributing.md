# 贡献指南

欢迎为 RushChat 项目做出贡献！

## 如何贡献

### 报告 Bug

1. 在 GitHub 提交 Issue
2. 描述问题
3. 提供复现步骤
4. 提供环境信息

### 提交功能请求

1. 在 GitHub 提交 Issue
2. 描述功能需求
3. 说明使用场景
4. 讨论实现方案

### 提交代码

1. Fork 项目
2. 创建功能分支
3. 提交更改
4. 创建 Pull Request

## 开发流程

### 1. Fork 项目

```bash
# Fork 到你的 GitHub 账号
# 然后克隆
git clone https://github.com/your-username/RustChat.git
cd RustChat
```

### 2. 创建功能分支

```bash
git checkout -b feature/your-feature-name
```

### 3. 开发

- 编写代码
- 添加测试
- 更新文档

### 4. 提交更改

```bash
git add .
git commit -m "描述你的更改"
git push origin feature/your-feature-name
```

### 5. 创建 Pull Request

1. 在 GitHub 创建 Pull Request
2. 描述更改内容
3. 等待代码审查

## 代码规范

### Rust

- 使用 `cargo fmt` 格式化
- 使用 `cargo clippy` 检查
- 添加必要的注释

### JavaScript

- 使用 ESLint
- 使用 Prettier
- 遵循 React Hooks 规则

### 提交信息

使用清晰的提交信息：

```
feat: 添加新功能
fix: 修复 Bug
docs: 更新文档
style: 代码格式
refactor: 重构
test: 添加测试
chore: 构建/工具
```

## 测试

### 后端测试

```bash
cd server-rust
cargo test
```

### 前端测试

```bash
cd client
npm test
```

## 相关文档

- [开发环境](setup.md)
- [代码结构](structure.md)
