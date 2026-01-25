# Red Packets

RushChat supports sending and claiming red packets, implemented based on smart contracts.

## Red Packet System Overview

```markmap
# Red Packet System
## Supported Chains
- EVM Chains
  - Ethereum
  - BSC
  - Polygon
- Solana Chain
  - Solana Mainnet
## Red Packet Types
- Regular Red Packet
  - Equal Distribution
  - Fixed Amount
- Random Red Packet
  - Random Distribution
  - Random Amount
## Send Process
- Select Type
- Set Amount
- Set Quantity
- Select Chain
- Connect Wallet
- On-chain Transaction
## Claim Process
- View Red Packet
- Connect Wallet
- Confirm Claim
- On-chain Transaction
- Receive Funds
## Red Packet Status
- Available
- Claimed Out
- Expired
## Technical Implementation
- Smart Contracts
  - EVM Contracts
  - Solana Programs
- X402 Protocol
  - Payment Verification
  - On-chain Settlement
```

## Red Packet Types

### EVM Chain Red Packets

Supports Ethereum, BSC, Polygon and other EVM chains.

### Solana Red Packets

Supports Solana mainnet.

## Send Red Packet

### Send Steps

1. Click red packet icon in chat interface
2. Select red packet type (Regular Red Packet/Random Red Packet)
3. Enter red packet amount and quantity
4. Select chain (EVM or Solana)
5. Connect wallet
6. Confirm send

### Red Packet Settings

- **Total Amount**: Total red packet amount
- **Quantity**: Number of red packets
- **Type**:
  - Regular Red Packet: Equal distribution
  - Random Red Packet: Random distribution

### On-chain Transaction

- Funds directly transferred to smart contract
- Need to pay Gas fees
- Red packet created successfully after transaction confirmation

## Claim Red Packet

### Claim Steps

1. See red packet message
2. Click "Claim" button
3. Connect wallet (if not connected)
4. Confirm claim
5. Wait for on-chain transaction confirmation

### Claim Limits

- Each red packet can only be claimed once
- Need to pay Gas fees (when claiming)
- Must claim within validity period

## Red Packet Status

### Available

- Red packet still has remaining
- User hasn't claimed
- Within validity period

### Claimed Out

- All shares have been claimed
- Display claim statistics

### Expired

- Exceeded validity period
- Cannot claim

## Red Packet Records

### Send Records

- View all sent red packets
- Display claim status
- Display total amount and remaining amount

### Claim Records

- View all claimed red packets
- Display claim amount
- Display sender information

## Related Documentation

- [X402 Protocol](x402-protocol.md)
- [Real-time Chat](../user-guide/chat.md)
