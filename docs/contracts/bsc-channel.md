# BSC 频道创建合约更新说明

## 问题分析

1. **BNB 支付失败原因**：前端代码只是简单转账，没有调用合约
2. **功能缺失**：EVM 合约缺少邀请者返佣功能（Solana 合约已有）

## 已完成的更新

### 1. EVM 合约更新 (`contracts/contracts/ChannelCreation.sol`)

#### 新增功能：
- ✅ 添加邀请者返佣功能（与 Solana 合约逻辑一致）
- ✅ 新增 `createChannelWithReferrer` 函数
- ✅ 保留 `createChannel` 函数（无邀请者版本）

#### 分配逻辑（与 Solana 一致）：
- **有邀请者**：
  - 30% 给邀请者
  - 70% 给平台 → 平台再分配：30%销毁，50%开发者，20%建设者
- **无邀请者**：
  - 100% 给平台 → 平台分配：30%销毁，50%开发者，20%建设者

#### 数据结构更新：
```solidity
struct ChannelCreationData {
    address creator;
    address referrer;          // 新增：邀请者地址
    uint256 totalAmount;
    uint256 referrerAmount;   // 新增：邀请者金额
    uint256 burnAmount;
    uint256 developerAmount;
    uint256 builderAmount;
    bool exists;
}
```

#### 事件更新：
```solidity
event ChannelCreated(
    string indexed channelId,
    address indexed creator,
    address indexed referrer,      // 新增
    uint256 totalAmount,
    uint256 referrerAmount,        // 新增
    uint256 burnAmount,
    uint256 developerAmount,
    uint256 builderAmount
);
```

### 2. 前端代码更新 (`client/src/components/CryptoPaymentModal.js`)

#### 新增功能：
- ✅ BNB 支付时调用合约（而不是简单转账）
- ✅ 支持邀请者返佣参数
- ✅ 从后端 API 获取合约地址

#### 实现逻辑：
1. 检查是否是频道创建支付（`isChannelCreation && currency === 'BNB'`）
2. 从后端 API 获取合约地址：`/api/config/channel-creation-addresses?chainId=97`
3. 使用 `viem` 编码函数调用
4. 调用 `createChannelWithReferrer` 函数

## 待完成的工作

### 1. 部署合约到 BSC 测试网

```bash
cd contracts
npx hardhat compile
npx hardhat run scripts/deploy.js --network bscTestnet
```

部署时需要提供以下参数：
- `_burnAddress`: 黑洞地址（用于销毁）
- `_developerWallet`: 开发者钱包地址
- `_builderWallet`: 建设者激励钱包地址
- `_tokenContract`: Token 合约地址（用于回购）

### 2. 配置环境变量

在 `.env` 文件中添加：
```bash
# BSC 频道创建合约地址
BSC_CHANNEL_CREATION_CONTRACT_ADDRESS=0x...  # 部署后的合约地址

# BSC 分配地址
BSC_BURN_ADDRESS=0x000000000000000000000000000000000000dEaD
BSC_DEVELOPER_ADDRESS=0x...  # 开发者地址
BSC_BUILDER_ADDRESS=0x...    # 建设者地址
```

### 3. 更新后端 API

在 `server-rust/src/handlers/config.rs` 中添加 BSC 合约地址返回逻辑：

```rust
// 在 get_channel_creation_addresses 函数中添加 BSC 支持
if chain_id == 97 || chain_id == 56 {
    let contract_address = std::env::var("BSC_CHANNEL_CREATION_CONTRACT_ADDRESS")
        .or_else(|_| std::env::var("BSC_RECIPIENT_ADDRESS"));
    
    let burn_address = std::env::var("BSC_BURN_ADDRESS")
        .unwrap_or_else(|_| "0x000000000000000000000000000000000000dEaD".to_string());
    
    let developer_address = std::env::var("BSC_DEVELOPER_ADDRESS")
        .unwrap_or_else(|_| "".to_string());
    
    let builder_address = std::env::var("BSC_BUILDER_ADDRESS")
        .unwrap_or_else(|_| "".to_string());
    
    // 返回 JSON 响应
}
```

### 4. 更新前端默认地址

在 `CryptoPaymentModal.js` 中更新默认合约地址：
```javascript
const DEFAULT_CONTRACT_ADDRESS = '0x...'; // 部署后的合约地址
const DEFAULT_DEVELOPER_ADDRESS = '0x...'; // 开发者地址
const DEFAULT_BUILDER_ADDRESS = '0x...';   // 建设者地址
```

## 测试步骤

1. **部署合约**到 BSC 测试网
2. **配置环境变量**（合约地址和分配地址）
3. **更新后端 API**以返回 BSC 合约地址
4. **测试频道创建**：
   - 无邀请者：验证分配是否正确（30%销毁，50%开发者，20%建设者）
   - 有邀请者：验证分配是否正确（30%邀请者，21%销毁，35%开发者，14%建设者）

## 注意事项

1. **Gas 限制**：合约调用需要更多 gas，已设置为 100000
2. **金额精度**：BNB 使用 18 位小数（1 BNB = 1e18 wei）
3. **合约地址验证**：确保合约地址格式正确（0x + 40 个十六进制字符）
4. **邀请者地址**：如果没有邀请者，传递 `0x0000000000000000000000000000000000000000`

## 交易失败分析

根据提供的交易链接：`https://testnet.bscscan.com/tx/0x0f33cbd1b4e5bc0f86cfbf2d278a5764ae2d695e08450429d6deda1a02d91647`

可能的原因：
1. 只是简单转账，没有调用合约
2. 合约未部署或地址错误
3. Gas 不足
4. 合约逻辑错误

更新后的代码将：
- ✅ 调用合约而不是简单转账
- ✅ 自动分配资金（邀请者、销毁、开发者、建设者）
- ✅ 与 Solana 合约逻辑一致
