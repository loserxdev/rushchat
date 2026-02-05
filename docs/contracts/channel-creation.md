# BSC 频道创建合约部署指南

## 概述

本指南说明如何部署 BSC 频道创建合约，并自动更新环境变量配置。

## 前置要求

1. **Node.js** 和 **npm** 已安装
2. **Hardhat** 已配置
3. **BSC 测试网账户**，有足够的 BNB 支付 Gas
4. **私钥**已配置在环境变量中

## 配置环境变量

在项目根目录的 `.env` 文件中配置以下变量：

```bash
# 部署账户私钥（用于支付 Gas）
PRIVATE_KEY=your_private_key_here

# BSC RPC URL（测试网）
BSC_TESTNET_RPC_URL=https://data-seed-prebsc-1-s1.binance.org:8545

# BSC 分配地址（部署前必须配置）
BSC_BURN_ADDRESS=0x000000000000000000000000000000000000dEaD  # 黑洞地址
BSC_DEVELOPER_ADDRESS=0x...  # 开发者钱包地址（必须配置）
BSC_BUILDER_ADDRESS=0x...    # 建设者激励钱包地址（必须配置）

# Token 合约地址（可选，用于回购）
BSC_TOKEN_CONTRACT=0x...      # Token 合约地址（如果不需要回购，可以设为零地址）

# BSCScan API Key（用于合约验证，可选）
BSCSCAN_API_KEY=your_bscscan_api_key
```

## 部署步骤

### 1. 编译合约

```bash
cd contracts
npm run compile
```

### 2. 部署到 BSC 测试网

```bash
npm run deploy:channel-creation:bsc-testnet
```

### 3. 部署到 BSC 主网（生产环境）

```bash
npm run deploy:channel-creation:bsc-mainnet
```

## 部署后自动更新

部署脚本会自动：

1. ✅ **更新根目录 `.env` 文件**，添加以下环境变量：
   ```bash
   BSC_CHANNEL_CREATION_CONTRACT_ADDRESS=0x...
   BSC_BURN_ADDRESS=0x...
   BSC_DEVELOPER_ADDRESS=0x...
   BSC_BUILDER_ADDRESS=0x...
   ```

2. ✅ **添加链特定配置**（用于多链支持）：
   ```bash
   BSC_CHANNEL_CREATION_CONTRACT_ADDRESS_97=0x...  # 测试网
   BSC_CHANNEL_CREATION_CONTRACT_ADDRESS_56=0x...   # 主网
   ```

3. ✅ **验证合约代码**（如果配置了 BSCScan API Key）

## 环境变量读取

### 后端（Rust）

后端会自动从根目录 `.env` 文件读取环境变量：

```rust
// server-rust/src/handlers/config.rs
let contract_address = std::env::var("BSC_CHANNEL_CREATION_CONTRACT_ADDRESS")
    .or_else(|_| std::env::var("BSC_RECIPIENT_ADDRESS"));
```

### 前端（React）

前端通过 `craco.config.js` 从根目录 `.env` 读取并注入到代码中：

```javascript
// client/craco.config.js
const bscChannelCreationContract = process.env.BSC_CHANNEL_CREATION_CONTRACT_ADDRESS || '';
```

前端代码中可以直接使用：
```javascript
// client/src/components/CryptoPaymentModal.js
const contractAddress = process.env.BSC_CHANNEL_CREATION_CONTRACT_ADDRESS || '';
```

## 验证部署

部署成功后，检查：

1. **合约地址**：部署脚本会输出合约地址
2. **环境变量**：检查根目录 `.env` 文件是否已更新
3. **API 端点**：访问 `/api/config/channel-creation-addresses?chainId=97` 应该返回合约地址
4. **前端调用**：尝试创建频道，应该能成功调用合约

## 故障排除

### 问题：部署失败，提示 "BSC_DEVELOPER_ADDRESS 未配置"

**解决方案**：在根目录 `.env` 文件中添加：
```bash
BSC_DEVELOPER_ADDRESS=0x...
BSC_BUILDER_ADDRESS=0x...
```

### 问题：环境变量未自动更新

**解决方案**：
1. 检查部署脚本是否有写入权限
2. 手动将合约地址添加到 `.env` 文件
3. 重启开发服务器

### 问题：前端无法读取环境变量

**解决方案**：
1. 确保环境变量在根目录 `.env` 文件中
2. 重启前端开发服务器（环境变量在构建时注入）
3. 检查 `craco.config.js` 是否正确配置

## 注意事项

1. **私钥安全**：永远不要将私钥提交到版本控制系统
2. **Gas 费用**：确保部署账户有足够的 BNB/ETH
3. **合约验证**：部署后建议验证合约代码，方便在区块浏览器查看
4. **多链支持**：脚本会自动添加链特定配置，支持多链部署

## 相关文件

- 部署脚本：`contracts/scripts/deploy-channel-creation.js`
- 合约代码：`contracts/contracts/ChannelCreation.sol`
- 前端配置：`client/craco.config.js`
- 后端 API：`server-rust/src/handlers/config.rs`
