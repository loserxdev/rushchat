# Wallet Verification

RushChat supports wallet address verification for channel rule verification.

## Wallet Verification Overview

```markmap
# Wallet Verification System
## Supported Wallets
- EVM Wallets
  - MetaMask
  - OKX Wallet
  - Coinbase Wallet
  - Trust Wallet
  - Rabby Wallet
  - WalletConnect
- Solana Wallets
  - Phantom
  - OKX Wallet (Solana)
  - Solflare
## Verification Types
- NFT Holder Verification
  - Single NFT
  - Collection Verification
  - Metaplex Core
- Token Holder Verification
  - Minimum Balance
  - ERC20/SPL Token
## Verification Process
- Connect Wallet
- Select Rule
- Auto Verification
  - RPC Call
  - DAS API
  - On-chain Query
- Verification Result
  - Pass/Fail
  - Error Prompt
## Technical Implementation
- EVM Chains
  - getBalance
  - balanceOf
  - ownerOf
- Solana Chain
  - getAssetsByOwner
  - DAS API
  - RPC Fallback
```

## Supported Wallets

### EVM Wallets

- MetaMask
- OKX Wallet
- Coinbase Wallet
- Trust Wallet
- Rabby Wallet
- WalletConnect

### Solana Wallets

- Phantom
- OKX Wallet (Solana)
- Solflare

## Connect Wallet

### Connect EVM Wallet

1. Click "Connect Wallet" button
2. Select wallet type (e.g., MetaMask)
3. Confirm connection in wallet
4. Address automatically saved after successful connection

### Connect Solana Wallet

1. Click "Connect Wallet" button
2. Select Solana wallet (e.g., Phantom)
3. Confirm connection in wallet
4. Address automatically saved after successful connection

## Wallet Verification

### NFT Holder Verification

Channels can set NFT holder requirements:

- Need to hold specified NFT
- Supports EVM chains and Solana
- Automatically verifies NFTs in wallet

### Token Holder Verification

Channels can set Token holder requirements:

- Need to hold specified amount of Token
- Supports EVM chains and Solana
- Automatically verifies wallet balance

### Collection Verification

Channels can set collection holder requirements:

- Need to hold any NFT from collection
- Supports Solana collections
- ✅ Uses DAS API (Digital Asset Standard API) for verification
- ✅ Supports Metaplex Core NFT standard
- ✅ Automatically detects if RPC endpoint supports DAS API
- ✅ Automatically falls back to Helius RPC if DAS API not supported

## Verification Process

### Verify When Joining Channel

1. Click join channel
2. If channel has verification rules, display verification prompt
3. Connect wallet (if not connected)
4. System automatically verifies
5. Can join after verification passes

### Verification Failed

If verification fails:

- Display failure reason
- Prompt required NFT/Token to hold
- Provide purchase link (if configured)

## Wallet Address Management

### Set Wallet Address

1. Enter profile
2. Enter wallet address in corresponding field
3. System automatically validates format
4. Save address

### Address Format

- **EVM**: `0x` prefixed 42 characters
- **Solana**: Base58 encoded, 32-44 characters

## Related Documentation

- [Channel System](../user-guide/channels.md)
- [Profile](../user-guide/profile.md)
