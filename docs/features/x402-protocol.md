# X402 Protocol

RushChat implements the Coinbase X402 protocol for payment and resource access control.

## X402 Protocol Overview

```markmap
# X402 Protocol
## Protocol Overview
- Web Payment Protocol
- Cryptocurrency Payment
- Resource Access Control
- Coinbase Standard
## Core Principles
- Gas Abstraction
  - Facilitator Handles
  - Users Don't Need to Consider
- Ease of Use
  - 10x Better Experience
  - Simplified Process
## Protocol Flow
- Client Request
  - GET /api/resource
- Server Response
  - HTTP 402
  - PAYMENT-REQUIRED header
- Client Payment
  - Create Transaction
  - On-chain Payment
  - PAYMENT-SIGNATURE
- Server Verification
  - Transaction Hash
  - Transaction Amount
  - Recipient
  - On-chain Status
- Return Resource
  - HTTP 200
  - PAYMENT-RESPONSE
## Current Implementation
- Standards Compliant
  - HTTP 402 Status Code
  - Standard Headers
  - On-chain Transactions
  - Transaction Verification
- Optional Optimizations
  - Facilitator (Not Implemented)
  - Batch Payments (Planned)
  - Payment Subscriptions (Planned)
## Gas Fees
- Current Implementation
  - User Pays (Send)
  - Platform Pays (Claim)
- Ideal State
  - Facilitator Pays
  - User Only Signs
```

## Protocol Overview

X402 is an open protocol for web payments, allowing clients to access protected resources through cryptocurrency payments.

## Core Principles

According to the [Coinbase X402 Protocol](https://github.com/coinbase/x402):

> **"Easy to use: x402 needs to be 10x better than existing ways to pay on the internet. This means abstracting as many details of crypto as possible away from the client and resource server, and into the facilitator."**

Key point: Gas fees should be handled by the Facilitator, clients and resource servers don't need to consider Gas.

## Protocol Flow

### 1. Client Requests Resource

```
GET /api/resource
```

### 2. Server Returns 402

```
HTTP/1.1 402 Payment Required
PAYMENT-REQUIRED: {
  "amount": "1000000000000000000",
  "currency": "ETH",
  "chainId": 1,
  "recipient": "0x..."
}
```

### 3. Client Provides Payment Proof

```
POST /api/resource
PAYMENT-SIGNATURE: <signature>
```

### 4. Server Verifies Payment

- Verify transaction hash
- Verify transaction amount
- Verify transaction recipient
- Verify on-chain status

### 5. Return Resource

```
HTTP/1.1 200 OK
PAYMENT-RESPONSE: {
  "txHash": "0x...",
  "verified": true
}
```

## Current Implementation

### X402 Standards Compliant

- ✅ Uses HTTP 402 status code
- ✅ Uses PAYMENT-REQUIRED header
- ✅ Uses PAYMENT-SIGNATURE header
- ✅ Uses PAYMENT-RESPONSE header
- ✅ Data structure complies with standards
- ✅ Real on-chain transactions
- ✅ Transaction verification

### Optional Optimizations

- ⚠️ Facilitator (Gas abstraction): Currently not implemented, but this is optional
- ⚠️ Batch payments: Planned
- ⚠️ Payment subscriptions: Planned

## Gas Fees

### Current Implementation

- User pays Gas (when sending red packet)
- Platform pays Gas (when claiming red packet)

### Ideal State (Using Facilitator)

- Facilitator pays Gas
- User only needs to sign authorization
- Better user experience

## Related Documentation

- [Red Packet System](red-packets.md)
- [X402 Gas Fees Explanation](https://github.com/Yukitojp/RustChat/blob/main/docs/features/x402-gas-fees-explanation.md)
