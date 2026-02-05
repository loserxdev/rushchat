# BSC_TOKEN_CONTRACT 说明

## 作用

`BSC_TOKEN_CONTRACT` 是用于 **Token 回购销毁功能** 的合约地址。

### 当前状态

- **当前未使用**：合约中已预留此参数，但回购功能尚未实现（标记为 TODO）
- **可选参数**：可以设置为零地址 `0x0000000000000000000000000000000000000000`

### 未来用途

当实现 Token 回购销毁功能时，此地址将用于：

1. **回购 Token**：使用 BNB/ETH 从 DEX（如 PancakeSwap）购买 Token
2. **销毁 Token**：将购买的 Token 发送到黑洞地址进行销毁
3. **通缩机制**：通过回购销毁减少 Token 总供应量

### 合约中的相关代码

```solidity
// contracts/contracts/ChannelCreation.sol

address public tokenContract; // Token合约地址（用于回购）

/**
 * @notice 执行Token回购并销毁（由后端或定时任务调用）
 * @dev 需要集成DEX进行swap，然后将Token发送到黑洞地址
 */
function buybackAndBurn(uint256 amount) external onlyOwner {
    // TODO: 集成DEX（如PancakeSwap）进行swap
    // 1. 将BNB/ETH swap为Token
    // 2. 将Token发送到黑洞地址（burnAddress）
}
```

## 部署脚本更新

部署脚本已更新，会自动将 `BSC_TOKEN_CONTRACT` 写入 `.env` 文件：

```javascript
const envVars = {
    'BSC_CHANNEL_CREATION_CONTRACT_ADDRESS': contractAddress,
    'BSC_BURN_ADDRESS': burnAddress,
    'BSC_DEVELOPER_ADDRESS': developerAddress,
    'BSC_BUILDER_ADDRESS': builderAddress,
    'BSC_TOKEN_CONTRACT': tokenContract, // ✅ 已添加
};
```

## 当前配置

在 `.env` 文件中：

```bash
# Token 合约地址（用于回购，当前未使用，可设为零地址）
BSC_TOKEN_CONTRACT=0x0000000000000000000000000000000000000000
```

## 注意事项

1. **当前功能**：频道创建和资金分配功能**不依赖**此参数
2. **未来扩展**：当需要实现 Token 回购时，再配置实际的 Token 合约地址
3. **零地址有效**：合约已修改，允许 `tokenContract` 为零地址

## 相关文件

- 合约代码：`contracts/contracts/ChannelCreation.sol`
- 部署脚本：`contracts/scripts/deploy-channel-creation.js`
- 环境变量：根目录 `.env`
