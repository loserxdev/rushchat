# 智能合约

RushChat 使用智能合约在 EVM 链和 Solana 上实现红包功能。本文档提供合约实现的详细技术信息。

## 概述

```markmap
# 智能合约
## EVM 合约
- Solidity 实现
  - RedPacket.sol
  - 函数
    - createRedPacket
    - claimRedPacket
    - refundExpired
    - withdrawUnclaimed
  - 事件
    - RedPacketCreated
    - RedPacketClaimed
## Solana 程序
- Rust 实现
  - lib.rs
  - 指令
    - CreateRedPacket
    - ClaimRedPacket
    - RefundExpired
  - PDA 账户
  - 数据结构
## 功能特性
- 随机分配
- 平均分配
- 过期处理
- 退款机制
- 链上存储
```

## EVM 智能合约 (Solidity)

### 合约地址

合约部署在多个 EVM 链上：

- **BSC 测试网**: `0x...` (需配置)
- **BSC 主网**: `0x...` (需配置)
- **Ethereum Goerli**: `0x...` (需配置)
- **Polygon Mumbai**: `0x...` (需配置)

### 合约接口

#### 函数

##### `createRedPacket`

在链上创建新红包。

```solidity
function createRedPacket(
    string memory packetId,
    uint256 numRecipients,
    bool randomized,
    uint256 deadline
) external payable
```

**参数：**
- `packetId`: 红包唯一标识符（字符串）
- `numRecipients`: 接收者数量（uint256）
- `randomized`: 是否使用随机分配（布尔值）
  - `true`: 随机分配（拼手气红包）
  - `false`: 平均分配（普通红包）
- `deadline`: 过期时间戳（uint256）

**要求：**
- `msg.value > 0`: 必须随交易发送资金
- `numRecipients > 0`: 必须至少有一个接收者
- `deadline > block.timestamp`: 过期时间必须在未来
- `!redPackets[packetId].exists`: 红包 ID 必须唯一

**事件：**
- 发出 `RedPacketCreated` 事件，包含红包详情

##### `claimRedPacket`

领取红包并接收分配的金额。

```solidity
function claimRedPacket(string memory packetId) external
```

**参数：**
- `packetId`: 红包唯一标识符（字符串）

**要求：**
- 红包必须存在
- 调用者之前不能领取过
- 红包不能已全部领取
- 红包不能已过期
- 红包必须有剩余金额

**分配逻辑：**

**随机分配：**
- 使用区块时间戳、prevrandao、发送者地址、红包 ID 和领取次数生成随机数
- 随机范围：平均金额的 0.1 倍到 1.9 倍
- 最后一个领取者获得全部剩余金额
- 确保每次领取至少 1 wei
- 防止领取导致剩余资金不足以支付其他领取者

**平均分配：**
- 将剩余金额平均分配给剩余接收者
- 最后一个领取者可能因舍入获得稍多金额

**事件：**
- 发出 `RedPacketClaimed` 事件，包含领取者地址、金额和剩余数量

##### `refundExpired`

将过期的红包退还给创建者。

```solidity
function refundExpired(string memory packetId) external
```

**参数：**
- `packetId`: 红包唯一标识符（字符串）

**要求：**
- 红包必须存在
- `block.timestamp > deadline`: 红包必须已过期
- `remainingAmount > 0`: 必须有剩余金额

**行为：**
- 将所有剩余金额转给创建者
- 将剩余金额设置为 0

##### `withdrawUnclaimed`

允许创建者在 5 分钟后提取未领取的金额。

```solidity
function withdrawUnclaimed(string memory packetId) external
```

**参数：**
- `packetId`: 红包唯一标识符（字符串）

**要求：**
- 红包必须存在
- `msg.sender == creator`: 只有创建者可以提取
- `remainingAmount > 0`: 必须有剩余金额
- 必须在创建后至少 5 分钟（由前端强制执行）

##### 视图函数

###### `getRedPacket`

```solidity
function getRedPacket(string memory packetId) 
    external 
    view 
    returns (RedPacketData memory)
```

返回完整的红包数据结构。

###### `hasClaimed`

```solidity
function hasClaimed(string memory packetId, address claimer) 
    external 
    view 
    returns (bool)
```

检查地址是否已领取特定红包。

###### `getClaimAmount`

```solidity
function getClaimAmount(string memory packetId, address claimer) 
    external 
    view 
    returns (uint256)
```

返回特定地址领取的金额。

###### `getClaimers`

```solidity
function getClaimers(string memory packetId) 
    external 
    view 
    returns (address[] memory)
```

返回所有领取者地址数组。

### 数据结构

#### `RedPacketData`

```solidity
struct RedPacketData {
    address creator;              // 创建者地址
    uint256 totalAmount;          // 总金额（wei）
    uint256 remainingAmount;      // 剩余金额（wei）
    uint256 numRecipients;        // 接收者总数
    uint256 claimedCount;         // 已领取次数
    bool randomized;              // 随机分配标志
    uint256 deadline;             // 过期时间戳
    bool exists;                  // 存在标志
}
```

### 事件

#### `RedPacketCreated`

```solidity
event RedPacketCreated(
    string indexed packetId,
    address indexed creator,
    uint256 totalAmount,
    uint256 numRecipients,
    bool randomized,
    uint256 deadline
);
```

#### `RedPacketClaimed`

```solidity
event RedPacketClaimed(
    string indexed packetId,
    address indexed claimer,
    uint256 amount,
    uint256 remainingCount
);
```

### 状态变量

- `mapping(string => RedPacketData) public redPackets`: 存储红包数据
- `mapping(string => mapping(address => bool)) public claimed`: 跟踪领取状态
- `mapping(string => address[]) public claimers`: 领取者列表
- `mapping(string => mapping(address => uint256)) public claimAmounts`: 领取金额
- `address public owner`: 合约所有者（用于紧急情况）

## Solana 程序 (Rust)

### 程序 ID

程序部署在 Solana 网络上：

- **Solana Devnet**: `WT5vFH9enojJ8VVHvaYx1DfaPWAwmX9X8EFs5Rbvp1s`
- **Solana 主网**: (待部署)

### 指令

#### `CreateRedPacket`

使用 PDA（程序派生地址）创建新红包。

**账户：**
- `[writable, signer]` 创建者账户（资金源）
- `[writable]` 红包 PDA 账户（待创建）
- `[]` 系统程序
- `[]` 租金系统变量

**指令数据：**
```rust
CreateRedPacket {
    packet_id: String,        // 唯一标识符（最多 64 字符）
    num_recipients: u32,      // 接收者数量
    randomized: bool,         // 随机分配标志
    deadline: i64,           // 过期时间戳
    amount: u64,             // 金额（lamports，不包括租金）
}
```

**行为：**
- 创建 PDA 账户存储红包数据
- 从创建者转移资金到 PDA
- 初始化红包数据结构
- PDA 地址派生自：`[program_id, "red_packet", packet_id]`

#### `ClaimRedPacket`

领取红包并接收分配的金额。

**账户：**
- `[writable, signer]` 领取者账户
- `[writable]` 红包 PDA 账户
- `[]` 时钟系统变量

**指令数据：**
```rust
ClaimRedPacket {
    packet_id: String,        // 唯一标识符
}
```

**要求：**
- 红包必须存在
- 调用者之前不能领取过
- 红包不能已全部领取
- 红包不能已过期
- 红包必须有剩余金额

**分配逻辑：**

**随机分配：**
- 使用时钟时间戳、领取者地址、红包 ID 和领取次数生成随机数
- 随机范围：平均金额的 0.1 倍到 1.9 倍
- 最后一个领取者获得全部剩余金额
- 确保每次领取至少 1 lamport

**平均分配：**
- 将剩余金额平均分配给剩余接收者

**行为：**
- 将分配的金额转给领取者
- 更新红包状态
- 将领取者添加到领取者列表

#### `RefundExpired`

将过期的红包退还给创建者。

**账户：**
- `[signer]` 创建者账户
- `[writable]` 红包 PDA 账户
- `[]` 时钟系统变量

**指令数据：**
```rust
RefundExpired {
    packet_id: String,        // 唯一标识符
}
```

**要求：**
- 红包必须存在
- `clock.unix_timestamp > deadline`: 红包必须已过期
- `remaining_amount > 0`: 必须有剩余金额
- `msg.sender == creator`: 只有创建者可以退款

**行为：**
- 将所有剩余金额转给创建者
- 将剩余金额设置为 0

### 数据结构

#### `RedPacketData`

```rust
pub struct RedPacketData {
    pub creator: Pubkey,          // 创建者公钥（32 字节）
    pub total_amount: u64,        // 总金额（lamports，8 字节）
    pub remaining_amount: u64,   // 剩余金额（lamports，8 字节）
    pub num_recipients: u32,      // 接收者总数（4 字节）
    pub claimed_count: u32,      // 已领取次数（4 字节）
    pub randomized: bool,          // 随机分配标志（1 字节）
    pub deadline: i64,            // 过期时间戳（8 字节）
    pub packet_id: String,         // 唯一红包标识符（4 + len 字节）
    pub claimers: Vec<Pubkey>,     // 领取者公钥列表（4 + 32*N 字节）
}
```

**账户大小计算：**
```rust
pub fn calculate_size(packet_id_len: usize, max_claimers: usize) -> usize {
    32 +  // creator: Pubkey
    8 +   // total_amount: u64
    8 +   // remaining_amount: u64
    4 +   // num_recipients: u32
    4 +   // claimed_count: u32
    1 +   // randomized: bool
    8 +   // deadline: i64
    4 + packet_id_len +  // packet_id: String
    4 + (32 * max_claimers)  // claimers: Vec<Pubkey>
}
```

**常量：**
- `MAX_PACKET_ID_LEN`: 64 字符
- `MAX_CLAIMERS`: 1000 个领取者

### 程序错误

```rust
#[derive(Error, Debug, Copy, Clone)]
pub enum RedPacketError {
    #[error("Invalid instruction")]
    InvalidInstruction,
    #[error("Red packet does not exist")]
    RedPacketNotFound,
    #[error("Already claimed")]
    AlreadyClaimed,
    #[error("Red packet is fully claimed")]
    FullyClaimed,
    #[error("Red packet has expired")]
    Expired,
    #[error("No remaining amount")]
    NoRemainingAmount,
    #[error("Invalid packet ID length")]
    InvalidPacketIdLength,
    #[error("Too many claimers")]
    TooManyClaimers,
    #[error("Invalid amount")]
    InvalidAmount,
    #[error("Invalid deadline")]
    InvalidDeadline,
    #[error("Unauthorized")]
    Unauthorized,
}
```

### PDA 派生

红包 PDA 使用以下方式派生：

```rust
let (pda, bump) = Pubkey::find_program_address(
    &[
        b"red_packet",
        packet_id.as_bytes(),
    ],
    program_id,
);
```

## 对比：EVM vs Solana

| 功能 | EVM (Solidity) | Solana (Rust) |
|------|---------------|---------------|
| **语言** | Solidity | Rust |
| **存储** | 合约存储（映射） | PDA 账户 |
| **Gas/交易费用** | Gas 费用（ETH/BNB） | 交易费用（SOL） |
| **随机性** | `block.prevrandao` + `block.timestamp` | 时钟时间戳 + 账户数据 |
| **账户模型** | 基于地址 | 基于账户（PDA） |
| **数据大小限制** | 无明确限制 | 必须计算账户大小 |
| **退款机制** | 直接转账 | PDA 到创建者转账 |
| **领取跟踪** | 嵌套映射 | 账户数据中的向量 |

## 安全考虑

### EVM 合约

1. **重入保护**：使用 `transfer()` 限制 gas，防止重入
2. **随机性**：使用 `block.prevrandao`（Paris 升级后）获得更好的随机性
3. **访问控制**：仅所有者可用的函数用于紧急情况
4. **溢出保护**：Solidity 0.8.20 内置溢出检查

### Solana 程序

1. **账户验证**：所有账户在使用前都经过验证
2. **PDA 安全**：使用 PDA 确保账户所有权
3. **租金豁免**：账户必须保持租金豁免余额
4. **指令验证**：所有指令数据都经过验证
5. **错误处理**：全面的错误类型用于调试

## 与 X402 协议的集成

两个合约都与 X402 支付协议集成：

1. **支付验证**：后端验证链上交易
2. **支付要求**：服务器通过 X402 头返回支付要求
3. **链上结算**：资金存储在合约中，而非平台钱包
4. **去中心化**：平台不托管资金

## 部署

### EVM 合约部署

```bash
cd contracts
npm install
npx hardhat compile
npx hardhat deploy --network bsc-testnet
```

### Solana 程序部署

```bash
cd contracts/solana-red-packet
cargo build-sbf
./deploy.sh
```

## 测试

### EVM 合约测试

```bash
npx hardhat test
```

### Solana 程序测试

```bash
./test.sh
```

## 合约地址

### EVM 链

- **BSC 测试网**：通过环境变量 `RED_PACKET_CONTRACT_ADDRESS` 配置
- **BSC 主网**：通过环境变量 `RED_PACKET_CONTRACT_ADDRESS_MAINNET` 配置

### Solana 网络

- **Solana Devnet**: `WT5vFH9enojJ8VVHvaYx1DfaPWAwmX9X8EFs5Rbvp1s`
- **Solana 主网**: (待部署)

## 参考

- [EVM 合约源码](../contracts/contracts/RedPacket.sol)
- [Solana 程序源码](../contracts/solana-red-packet/src/lib.rs)
- [X402 协议文档](./x402-protocol.md)
- [红包功能指南](../features/red-packets.md)
