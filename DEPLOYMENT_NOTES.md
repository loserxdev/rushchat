# MkDocs 部署注意事项

## 中英文切换路径配置

### 问题说明

在生产环境中，如果 MkDocs 部署在子目录（如 GitHub Pages 项目站点），语言切换路径可能会出错。

### 解决方案

#### 1. 根目录部署

如果部署在根目录（如 `https://your-domain.com/`），使用以下配置：

```yaml
site_url: https://your-domain.com/
```

#### 2. 子目录部署

如果部署在子目录（如 `https://username.github.io/repository-name/`），**必须**包含子目录路径：

```yaml
site_url: https://username.github.io/repository-name/
```

**重要**：`site_url` 必须以 `/` 结尾，且必须包含完整的子目录路径。

### 配置检查

在 `mkdocs.yml` 中确保：

1. ✅ `site_url` 正确设置（包含子目录路径，如果适用）
2. ✅ `reconfigure_material: true` 已启用（自动处理语言切换）
3. ✅ `use_directory_urls: true` 已设置

### 验证

构建后检查生成的 HTML：

```bash
# 检查首页的语言切换链接
grep "md-select__link" site/index.html

# 检查子页面的语言切换链接
grep "md-select__link" site/installation/index.html
```

### 常见问题

**问题**：语言切换后出现 404 错误

**原因**：`site_url` 未包含子目录路径

**解决**：更新 `site_url` 为完整路径，例如：
- ❌ 错误：`site_url: https://username.github.io`
- ✅ 正确：`site_url: https://username.github.io/repository-name/`
