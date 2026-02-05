# 合约部署指南

## 📋 私钥配置步骤

### 1. 创建 `.env` 文件

在 `contracts/` 目录下创建 `.env` 文件：

```bash
cd contracts
cp .env.example .env
```

### 2. 配置私钥

编辑 `.env` 文件，设置 `PRIVATE_KEY`：

```bash
# 私钥格式：必须以 0x 开头，64 个十六进制字符
PRIVATE_KEY=0x你的私钥
```

**重要：**
- 私钥必须以 `0x` 开头
- 私钥长度必须是 66 个字符（包括 `0x`）
- 示例：`PRIVATE_KEY=0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef`

### 3. 获取测试网私钥

#### 方法 1: 使用 MetaMask

1. 打开 MetaMask
2. 选择测试网账户
3. 点击账户名称 → "账户详情"
4. 点击"导出私钥"
5. 输入密码后复制私钥

#### 方法 2: 使用命令行生成

```bash
# 使用 Node.js 生成随机私钥（仅用于测试）
node -e "console.log('0x' + require('crypto').randomBytes(32).toString('hex'))"
```

### 4. 确保钱包有足够的测试币

#### BSC 测试网 (BSC Testnet)

1. 访问 [BSC Testnet Faucet](https://testnet.bnbchain.org/faucet-smart)
2. 输入你的钱包地址
3. 获取测试 BNB

#### Ethereum Sepolia 测试网

1. 访问 [Sepolia Faucet](https://sepoliafaucet.com/)
2. 输入你的钱包地址
3. 获取测试 ETH

## 🚀 部署步骤

### 1. 安装依赖

```bash
cd contracts
npm install
```

### 2. 配置环境变量

确保 `.env` 文件已正确配置（见上方步骤）

### 3. 编译合约

```bash
npm run compile
```

### 4. 部署到测试网

#### BSC 测试网

```bash
npm run deploy:bsc-testnet
```

#### BSC 主网

```bash
npm run deploy:bsc-mainnet
```

#### Ethereum Sepolia 测试网

```bash
npm run deploy:sepolia
```

### 5. 保存部署信息

部署成功后，会输出：

```
RedPacket deployed to: 0x...
Network: bscTestnet
Chain ID: 97

=== Deployment Info ===
{
  "network": "bscTestnet",
  "chainId": "97",
  "contractAddress": "0x...",
  "deployer": "0x...",
  "timestamp": "2024-01-01T00:00:00.000Z"
}
```

**重要：保存这些信息！**

### 6. 自动更新环境变量

**✅ 部署脚本会自动更新 .env 文件！**

部署成功后，脚本会自动：
- 查找项目根目录或 `server-rust` 目录下的 `.env` 文件
- 如果 `.env` 文件不存在，会在项目根目录创建
- 自动更新或添加以下环境变量：
  - `RED_PACKET_CONTRACT_ADDRESS`（合约地址）
  - `RED_PACKET_CONTRACT_CHAIN_ID`（链 ID）

**无需手动配置！** 部署完成后，环境变量已自动更新。

如果自动更新失败，可以手动添加到 `.env` 文件：

```bash
# server-rust/.env 或项目根目录 .env
RED_PACKET_CONTRACT_ADDRESS=0x...  # 从部署输出中复制
RED_PACKET_CONTRACT_CHAIN_ID=97     # BSC Testnet
```

## 🔐 安全注意事项

### ⚠️ 私钥安全

1. **永远不要提交 `.env` 文件**
   - `.env` 已在 `.gitignore` 中
   - 确保不会意外提交到 Git

2. **使用测试钱包**
   - 测试网部署使用专门的测试钱包
   - 不要使用主网钱包的私钥

3. **主网部署**
   - 使用硬件钱包
   - 或使用安全的密钥管理服务（如 AWS Secrets Manager）
   - 考虑使用多签钱包

4. **私钥格式检查**
   ```bash
   # 验证私钥格式
   echo $PRIVATE_KEY | grep -E '^0x[0-9a-fA-F]{64}$'
   ```

### ✅ 部署前检查清单

- [ ] `.env` 文件已创建
- [ ] `PRIVATE_KEY` 已配置（格式正确）
- [ ] 钱包有足够的测试币（用于支付 Gas）
- [ ] RPC 端点已配置
- [ ] 已编译合约（无错误）
- [ ] 已保存部署信息（合约地址等）

## 🐛 常见问题

### 问题 1: "Invalid private key"

**原因：** 私钥格式不正确

**解决：**
- 确保私钥以 `0x` 开头
- 确保私钥长度为 66 个字符
- 检查是否有空格或换行符

### 问题 2: "insufficient funds for gas"

**原因：** 钱包余额不足

**解决：**
- 从测试网水龙头获取测试币
- 检查钱包地址是否正确

### 问题 3: "nonce too low"

**原因：** 网络状态不同步

**解决：**
- 等待几分钟后重试
- 检查 RPC 端点是否正常

### 问题 4: 合约验证失败

**原因：** Block Explorer API Key 未配置或无效

**解决：**
- 验证是可选的，不影响合约使用
- 如需验证，配置正确的 API Key

## 📚 相关文档

- [合约 README](https://github.com/Yukitojp/RustChat/tree/main/contracts)
- [智能合约实现方案](../features/red-packets.md)
