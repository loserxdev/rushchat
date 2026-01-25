# 钱包验证

RushChat 支持钱包地址验证，用于频道规则验证。

## 支持的钱包

### EVM 钱包

- MetaMask
- OKX Wallet
- Coinbase Wallet
- Trust Wallet
- Rabby Wallet
- WalletConnect

### Solana 钱包

- Phantom
- OKX Wallet（Solana）
- Solflare

## 连接钱包

### 连接 EVM 钱包

1. 点击"连接钱包"按钮
2. 选择钱包类型（如 MetaMask）
3. 在钱包中确认连接
4. 连接成功后地址自动保存

### 连接 Solana 钱包

1. 点击"连接钱包"按钮
2. 选择 Solana 钱包（如 Phantom）
3. 在钱包中确认连接
4. 连接成功后地址自动保存

## 钱包验证

### NFT 持有验证

频道可以设置 NFT 持有要求：

- 需要持有指定的 NFT
- 支持 EVM 链和 Solana
- 自动验证钱包中的 NFT

### Token 持有验证

频道可以设置 Token 持有要求：

- 需要持有指定数量的 Token
- 支持 EVM 链和 Solana
- 自动验证钱包余额

### 集合验证

频道可以设置集合持有要求：

- 需要持有集合中的任意 NFT
- 支持 Solana 集合
- 使用 DAS API 验证

## 验证流程

### 加入频道时验证

1. 点击加入频道
2. 如果频道有验证规则，显示验证提示
3. 连接钱包（如果未连接）
4. 系统自动验证
5. 验证通过后可以加入

### 验证失败

如果验证失败：

- 显示失败原因
- 提示需要持有的 NFT/Token
- 提供购买链接（如果配置）

## 钱包地址管理

### 设置钱包地址

1. 进入个人资料
2. 在相应字段输入钱包地址
3. 系统自动验证格式
4. 保存地址

### 地址格式

- **EVM**：`0x` 开头的 42 字符
- **Solana**：Base58 编码，32-44 字符

## 相关文档

- [频道系统](../user-guide/channels.md)
- [个人资料](../user-guide/profile.md)
