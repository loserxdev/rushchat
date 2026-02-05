# Smart Contracts

RushChat implements red packet functionality using smart contracts on both EVM chains and Solana. This document provides detailed technical information about the contract implementations.

## Overview

```markmap
# Smart Contracts
## EVM Contracts
- Solidity Implementation
  - RedPacket.sol
  - Functions
    - createRedPacket
    - claimRedPacket
    - refundExpired
    - withdrawUnclaimed
  - Events
    - RedPacketCreated
    - RedPacketClaimed
## Solana Programs
- Rust Implementation
  - lib.rs
  - Instructions
    - CreateRedPacket
    - ClaimRedPacket
    - RefundExpired
  - PDA Accounts
  - Data Structures
## Features
- Random Distribution
- Equal Distribution
- Expiration Handling
- Refund Mechanism
- On-chain Storage
```

## EVM Smart Contract (Solidity)

### Contract Address

The contract is deployed on multiple EVM chains:

- **BSC Testnet**: `0x...` (to be configured)
- **BSC Mainnet**: `0x...` (to be configured)
- **Ethereum Goerli**: `0x...` (to be configured)
- **Polygon Mumbai**: `0x...` (to be configured)

### Contract Interface

#### Functions

##### `createRedPacket`

Creates a new red packet on-chain.

```solidity
function createRedPacket(
    string memory packetId,
    uint256 numRecipients,
    bool randomized,
    uint256 deadline
) external payable
```

**Parameters:**
- `packetId`: Unique identifier for the red packet (string)
- `numRecipients`: Number of recipients (uint256)
- `randomized`: Whether to use random distribution (bool)
  - `true`: Random distribution (拼手气红包)
  - `false`: Equal distribution (普通红包)
- `deadline`: Expiration timestamp (uint256)

**Requirements:**
- `msg.value > 0`: Must send funds with the transaction
- `numRecipients > 0`: Must have at least one recipient
- `deadline > block.timestamp`: Deadline must be in the future
- `!redPackets[packetId].exists`: Packet ID must be unique

**Events:**
- Emits `RedPacketCreated` event with packet details

##### `claimRedPacket`

Claims a red packet and receives the allocated amount.

```solidity
function claimRedPacket(string memory packetId) external
```

**Parameters:**
- `packetId`: Unique identifier for the red packet (string)

**Requirements:**
- Packet must exist
- Caller must not have claimed before
- Packet must not be fully claimed
- Packet must not be expired
- Packet must have remaining amount

**Distribution Logic:**

**Random Distribution:**
- Uses block timestamp, prevrandao, sender address, packet ID, and claim count for randomness
- Random range: 0.1x to 1.9x of average amount
- Last recipient receives all remaining amount
- Ensures minimum 1 wei per claim
- Prevents claims that would leave insufficient funds for remaining recipients

**Equal Distribution:**
- Divides remaining amount equally among remaining recipients
- Last recipient may receive slightly more due to rounding

**Events:**
- Emits `RedPacketClaimed` event with claimer address, amount, and remaining count

##### `refundExpired`

Refunds expired red packet to creator.

```solidity
function refundExpired(string memory packetId) external
```

**Parameters:**
- `packetId`: Unique identifier for the red packet (string)

**Requirements:**
- Packet must exist
- `block.timestamp > deadline`: Packet must be expired
- `remainingAmount > 0`: Must have remaining amount

**Behavior:**
- Transfers all remaining amount to creator
- Sets remaining amount to 0

##### `withdrawUnclaimed`

Allows creator to withdraw unclaimed amount after 5 minutes.

```solidity
function withdrawUnclaimed(string memory packetId) external
```

**Parameters:**
- `packetId`: Unique identifier for the red packet (string)

**Requirements:**
- Packet must exist
- `msg.sender == creator`: Only creator can withdraw
- `remainingAmount > 0`: Must have remaining amount
- Must be at least 5 minutes after creation (enforced by frontend)

##### View Functions

###### `getRedPacket`

```solidity
function getRedPacket(string memory packetId) 
    external 
    view 
    returns (RedPacketData memory)
```

Returns complete red packet data structure.

###### `hasClaimed`

```solidity
function hasClaimed(string memory packetId, address claimer) 
    external 
    view 
    returns (bool)
```

Checks if an address has claimed a specific red packet.

###### `getClaimAmount`

```solidity
function getClaimAmount(string memory packetId, address claimer) 
    external 
    view 
    returns (uint256)
```

Returns the amount claimed by a specific address.

###### `getClaimers`

```solidity
function getClaimers(string memory packetId) 
    external 
    view 
    returns (address[] memory)
```

Returns array of all claimer addresses.

### Data Structures

#### `RedPacketData`

```solidity
struct RedPacketData {
    address creator;              // Creator's address
    uint256 totalAmount;          // Total amount in wei
    uint256 remainingAmount;      // Remaining amount in wei
    uint256 numRecipients;        // Total number of recipients
    uint256 claimedCount;         // Number of claims made
    bool randomized;              // Random distribution flag
    uint256 deadline;             // Expiration timestamp
    bool exists;                  // Existence flag
}
```

### Events

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

### State Variables

- `mapping(string => RedPacketData) public redPackets`: Stores red packet data
- `mapping(string => mapping(address => bool)) public claimed`: Tracks claim status
- `mapping(string => address[]) public claimers`: List of claimers
- `mapping(string => mapping(address => uint256)) public claimAmounts`: Claim amounts
- `address public owner`: Contract owner (for emergency)

## Solana Program (Rust)

### Program ID

The program is deployed on Solana networks:

- **Solana Devnet**: `WT5vFH9enojJ8VVHvaYx1DfaPWAwmX9X8EFs5Rbvp1s`
- **Solana Mainnet**: (to be deployed)

### Instructions

#### `CreateRedPacket`

Creates a new red packet using a PDA (Program Derived Address).

**Accounts:**
- `[writable, signer]` Creator account (funds source)
- `[writable]` Red packet PDA account (to be created)
- `[]` System program
- `[]` Rent sysvar

**Instruction Data:**
```rust
CreateRedPacket {
    packet_id: String,        // Unique identifier (max 64 chars)
    num_recipients: u32,      // Number of recipients
    randomized: bool,         // Random distribution flag
    deadline: i64,           // Expiration timestamp
    amount: u64,             // Amount in lamports (excluding rent)
}
```

**Behavior:**
- Creates PDA account to store red packet data
- Transfers funds from creator to PDA
- Initializes red packet data structure
- PDA address is derived from: `[program_id, "red_packet", packet_id]`

#### `ClaimRedPacket`

Claims a red packet and receives allocated amount.

**Accounts:**
- `[writable, signer]` Claimer account
- `[writable]` Red packet PDA account
- `[]` Clock sysvar

**Instruction Data:**
```rust
ClaimRedPacket {
    packet_id: String,        // Unique identifier
}
```

**Requirements:**
- Packet must exist
- Caller must not have claimed before
- Packet must not be fully claimed
- Packet must not be expired
- Packet must have remaining amount

**Distribution Logic:**

**Random Distribution:**
- Uses clock timestamp, claimer address, packet ID, and claim count for randomness
- Random range: 0.1x to 1.9x of average amount
- Last recipient receives all remaining amount
- Ensures minimum 1 lamport per claim

**Equal Distribution:**
- Divides remaining amount equally among remaining recipients

**Behavior:**
- Transfers allocated amount to claimer
- Updates red packet state
- Adds claimer to claimers list

#### `RefundExpired`

Refunds expired red packet to creator.

**Accounts:**
- `[signer]` Creator account
- `[writable]` Red packet PDA account
- `[]` Clock sysvar

**Instruction Data:**
```rust
RefundExpired {
    packet_id: String,        // Unique identifier
}
```

**Requirements:**
- Packet must exist
- `clock.unix_timestamp > deadline`: Packet must be expired
- `remaining_amount > 0`: Must have remaining amount
- `msg.sender == creator`: Only creator can refund

**Behavior:**
- Transfers all remaining amount to creator
- Sets remaining amount to 0

### Data Structures

#### `RedPacketData`

```rust
pub struct RedPacketData {
    pub creator: Pubkey,          // Creator's public key (32 bytes)
    pub total_amount: u64,        // Total amount in lamports (8 bytes)
    pub remaining_amount: u64,   // Remaining amount in lamports (8 bytes)
    pub num_recipients: u32,      // Total number of recipients (4 bytes)
    pub claimed_count: u32,      // Number of claims made (4 bytes)
    pub randomized: bool,          // Random distribution flag (1 byte)
    pub deadline: i64,            // Expiration timestamp (8 bytes)
    pub packet_id: String,         // Unique packet identifier (4 + len bytes)
    pub claimers: Vec<Pubkey>,     // List of claimer public keys (4 + 32*N bytes)
}
```

**Account Size Calculation:**
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

**Constants:**
- `MAX_PACKET_ID_LEN`: 64 characters
- `MAX_CLAIMERS`: 1000 claimers

### Program Errors

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

### PDA Derivation

The red packet PDA is derived using:

```rust
let (pda, bump) = Pubkey::find_program_address(
    &[
        b"red_packet",
        packet_id.as_bytes(),
    ],
    program_id,
);
```

## Comparison: EVM vs Solana

| Feature | EVM (Solidity) | Solana (Rust) |
|---------|---------------|---------------|
| **Language** | Solidity | Rust |
| **Storage** | Contract storage (mappings) | PDA accounts |
| **Gas/Transaction Fees** | Gas fees (ETH/BNB) | Transaction fees (SOL) |
| **Randomness** | `block.prevrandao` + `block.timestamp` | Clock timestamp + account data |
| **Account Model** | Address-based | Account-based (PDA) |
| **Data Size Limits** | No explicit limit | Account size must be calculated |
| **Refund Mechanism** | Direct transfer | PDA to creator transfer |
| **Claim Tracking** | Nested mappings | Vector in account data |

## Security Considerations

### EVM Contract

1. **Reentrancy Protection**: Uses `transfer()` which limits gas, preventing reentrancy
2. **Randomness**: Uses `block.prevrandao` (post-Paris upgrade) for better randomness
3. **Access Control**: Owner-only functions for emergency situations
4. **Overflow Protection**: Solidity 0.8.20 has built-in overflow checks

### Solana Program

1. **Account Validation**: All accounts are validated before use
2. **PDA Security**: Uses PDAs to ensure account ownership
3. **Rent Exemption**: Accounts must maintain rent-exempt balance
4. **Instruction Validation**: All instruction data is validated
5. **Error Handling**: Comprehensive error types for debugging

## Integration with X402 Protocol

Both contracts integrate with the X402 payment protocol:

1. **Payment Verification**: Backend verifies on-chain transactions
2. **Payment Requirements**: Server returns payment requirements via X402 headers
3. **On-chain Settlement**: Funds are stored in contracts, not platform wallets
4. **Decentralized**: No platform custody of funds

## Deployment

### EVM Contract Deployment

```bash
cd contracts
npm install
npx hardhat compile
npx hardhat deploy --network bsc-testnet
```

### Solana Program Deployment

```bash
cd contracts/solana-red-packet
cargo build-sbf
./deploy.sh
```

## Testing

### EVM Contract Tests

```bash
npx hardhat test
```

### Solana Program Tests

```bash
./test.sh
```

## Contract Addresses

### EVM Chains

- **BSC Testnet**: Configure via environment variable `RED_PACKET_CONTRACT_ADDRESS`
- **BSC Mainnet**: Configure via environment variable `RED_PACKET_CONTRACT_ADDRESS_MAINNET`

### Solana Networks

- **Solana Devnet**: `WT5vFH9enojJ8VVHvaYx1DfaPWAwmX9X8EFs5Rbvp1s`
- **Solana Mainnet**: (to be deployed)

## References

- [EVM Contract Source](https://github.com/Yukitojp/RustChat/blob/main/contracts/contracts/RedPacket.sol)
- [Solana Program Source](https://github.com/Yukitojp/RustChat/blob/main/contracts/solana-red-packet/src/lib.rs)
- [X402 Protocol Documentation](../features/x402-protocol.md)
- [Red Packets Feature Guide](../features/red-packets.md)
