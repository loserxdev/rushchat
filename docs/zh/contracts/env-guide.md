# .env 文件中文注释说明

## 概述

`.env` 文件中的所有 BSC 相关参数都已添加中文注释，说明每个参数的用途。

## BSC 配置参数说明

### RPC 配置

```bash
# BSC RPC 节点（主网，Chain ID: 56）
# BSC RPC Node (Mainnet, Chain ID: 56)
BSC_RPC=wss://rpc.particle.network/evm-chain?chainId=56&...
```

**用途**：BSC 主网 RPC 节点地址，用于连接 BSC 区块链网络。

### 频道创建合约配置

```bash
# ========== BSC 频道创建合约配置 ==========
# BSC Channel Creation Contract Configuration

# 频道创建合约地址（部署后自动更新）
# Channel Creation Contract Address (auto-updated after deployment)
BSC_CHANNEL_CREATION_CONTRACT_ADDRESS=0x...

# 黑洞地址（用于销毁，接收平台收入的30%）
# Burn Address (for token burn, receives 30% of platform revenue)
BSC_BURN_ADDRESS=0x...

# 开发者钱包地址（接收平台收入的50%）
# Developer Wallet Address (receives 50% of platform revenue)
BSC_DEVELOPER_ADDRESS=0x...

# 建设者激励钱包地址（接收平台收入的20%）
# Builder Incentive Wallet Address (receives 20% of platform revenue)
BSC_BUILDER_ADDRESS=0x...

# Token 合约地址（用于回购销毁，当前未使用，可设为零地址）
# Token Contract Address (for buyback and burn, currently unused, can be zero address)
BSC_TOKEN_CONTRACT=0x0000000000000000000000000000000000000000
```

### 测试网链特定配置

```bash
# ========== BSC 测试网链特定配置（Chain ID: 97）==========
# BSC Testnet Chain-Specific Configuration (Chain ID: 97)
# 注意：钱包地址（BURN、DEVELOPER、BUILDER、TOKEN）测试网与主网共用
# Note: Wallet addresses (BURN, DEVELOPER, BUILDER, TOKEN) are shared between testnet and mainnet

# 测试网频道创建合约地址
# Testnet Channel Creation Contract Address
BSC_CHANNEL_CREATION_CONTRACT_ADDRESS_97=0x...
```

**说明**：测试网与主网共用相同的钱包地址（`BSC_BURN_ADDRESS`、`BSC_DEVELOPER_ADDRESS`、`BSC_BUILDER_ADDRESS`、`BSC_TOKEN_CONTRACT`），仅合约地址需要区分。

## 自动更新

部署脚本 (`deploy-channel-creation.js`) 会自动：

1. ✅ **添加中文注释**：每个参数都有对应的中文说明
2. ✅ **更新环境变量**：部署后自动更新到 `.env` 文件
3. ✅ **保持格式**：注释格式统一，易于阅读

## 参数用途总结

| 参数 | 用途 | 必需 |
|------|------|------|
| `BSC_CHANNEL_CREATION_CONTRACT_ADDRESS` | 频道创建合约地址 | ✅ |
| `BSC_BURN_ADDRESS` | 黑洞地址（销毁，30%） | ✅ |
| `BSC_DEVELOPER_ADDRESS` | 开发者钱包（50%） | ✅ |
| `BSC_BUILDER_ADDRESS` | 建设者激励钱包（20%） | ✅ |
| `BSC_TOKEN_CONTRACT` | Token 合约（回购用，可选） | ❌ |

## 注意事项

1. **自动更新**：部署合约后，这些参数会自动更新到 `.env` 文件
2. **中文注释**：所有参数都有中文注释说明用途
3. **格式统一**：注释格式统一，便于维护
