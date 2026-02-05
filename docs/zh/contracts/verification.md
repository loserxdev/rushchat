# 合约验证指南

## 为什么需要验证合约？

验证合约后，BscScan 浏览器会：
- ✅ 显示源代码（而不是字节码）
- ✅ 显示函数名（如 `claimRedPacket`）而不是函数选择器（如 `0x1a3c57e6`）
- ✅ 提供交互式合约调用界面
- ✅ 显示完整的 ABI
- ✅ 提高合约透明度和可信度

## 快速验证步骤

### 1. 获取 BscScan API Key

1. 访问 [BscScan](https://bscscan.com/)（主网）或 [BscScan Testnet](https://testnet.bscscan.com/)（测试网）
2. 注册/登录账户
3. 进入 [API Keys 页面](https://bscscan.com/myapikey)
4. 点击 "Add" 创建新的 API Key
5. 复制 API Key

### 2. 配置 API Key

在 `contracts/.env` 文件中添加：

```bash
BSCSCAN_API_KEY=你的API密钥
```

### 3. 验证合约

#### 方法 A: 使用验证脚本（推荐）

```bash
# 设置合约地址
export RED_PACKET_CONTRACT_ADDRESS=0x你的合约地址

# BSC 测试网
npm run verify:bsc-testnet

# BSC 主网
npm run verify:bsc-mainnet
```

#### 方法 B: 使用 Hardhat 命令

```bash
# BSC 测试网
npx hardhat verify --network bscTestnet <合约地址>

# BSC 主网
npx hardhat verify --network bscMainnet <合约地址>
```

#### 方法 C: 部署时自动验证

部署脚本已包含自动验证功能。如果部署时验证失败，可以稍后手动验证。

### 4. 验证成功

验证成功后，你会看到：

```
✅ 合约验证成功！
🔗 可在 BscScan 查看: https://testnet.bscscan.com/address/0x...
```

## 常见问题

### Q: 验证失败，提示 "Already Verified"

**A:** 合约已经验证过了，无需重复验证。

### Q: 验证失败，提示 "Contract source code already verified"

**A:** 合约已经验证过了，这是正常提示。

### Q: 验证失败，提示 "Fail - Unable to verify"

**A:** 可能的原因：
1. API Key 未配置或无效
2. 合约地址错误
3. 网络问题
4. 合约部署后等待时间不够（需要至少 5 个区块确认）

**解决方案：**
- 检查 `.env` 文件中的 `BSCSCAN_API_KEY`
- 确认合约地址正确
- 等待几分钟后重试
- 检查网络连接

### Q: 如何手动验证？

如果自动验证失败，可以：

1. 访问 BscScan 合约地址页面
2. 点击 "Contract" 标签
3. 点击 "Verify and Publish"
4. 选择 "Solidity (Single file)" 或 "Solidity (Standard JSON Input)"
5. 填写合约信息并上传源代码

### Q: 验证后多久生效？

通常验证后立即生效，最多等待 1-2 分钟。

## 验证后的效果对比

### 验证前
- 显示：`0x1a3c57e6`（函数选择器）
- 无法查看源代码
- 无法交互式调用

### 验证后
- 显示：`claimRedPacket(string)`（函数名和参数）
- 可以查看完整源代码
- 可以交互式调用合约函数
- 显示完整的 ABI

## 注意事项

1. **API Key 安全**
   - 不要将 API Key 提交到代码仓库
   - API Key 仅用于验证，不会影响合约安全性

2. **验证时机**
   - 建议部署后立即验证
   - 如果部署时验证失败，可以稍后手动验证

3. **多链部署**
   - 每个链需要单独验证
   - 使用对应的 API Key（BscScan 主网和测试网使用同一个 API Key）
