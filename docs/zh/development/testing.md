# 测试指南

RushChat 的测试说明。

## 测试概览

```markmap
# 测试指南
## 测试类型
- 单元测试
  - 单个函数
  - 单个模块
  - 快速执行
- 集成测试
  - 多个模块
  - 模块协作
  - 接口测试
- 端到端测试
  - 完整流程
  - 用户场景
  - 系统测试
## 后端测试
- 运行测试
  - cargo test
  - 测试套件
- 编写测试
  - #[cfg(test)]
  - #[test]
  - 断言
## 前端测试
- 运行测试
  - npm test
  - Jest
- 编写测试
  - 组件测试
  - 工具函数测试
## 测试覆盖
- 代码覆盖率
- 功能覆盖
- 边界测试
```

## 测试类型

### 单元测试

测试单个函数或模块。

### 集成测试

测试多个模块的协作。

### 端到端测试

测试完整的用户流程。

## 后端测试

### 运行测试

```bash
cd server-rust
cargo test
```

### 编写测试

在 Rust 文件中添加测试：

```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_function() {
        // 测试代码
    }
}
```

## 前端测试

### 运行测试

```bash
cd client
npm test
```

### 编写测试

使用 React Testing Library：

```javascript
import { render, screen } from '@testing-library/react';
import Component from './Component';

test('renders component', () => {
  render(<Component />);
  expect(screen.getByText('Hello')).toBeInTheDocument();
});
```

## 手动测试

### 功能测试清单

- [ ] 用户注册和登录
- [ ] 发送和接收消息
- [ ] 创建和加入频道
- [ ] 钱包连接
- [ ] 红包发送和领取
- [ ] 管理员操作

## 相关文档

- [开发环境](setup.md)
- [代码结构](structure.md)
