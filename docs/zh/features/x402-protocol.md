# X402 协议

RushChat 实现了 Coinbase X402 协议，用于支付和资源访问控制。

## X402 协议概览

```markmap
# X402 协议
## 协议概述
- Web支付协议
- 加密货币支付
- 资源访问控制
- Coinbase标准
## 核心原则
- Gas抽象
  - Facilitator处理
  - 用户无需考虑
- 易用性
  - 10x更好体验
  - 简化流程
## 协议流程
- 客户端请求
  - GET /api/resource
- 服务器响应
  - HTTP 402
  - PAYMENT-REQUIRED header
- 客户端支付
  - 创建交易
  - 链上支付
  - PAYMENT-SIGNATURE
- 服务器验证
  - 交易哈希
  - 交易金额
  - 接收者
  - 链上状态
- 返回资源
  - HTTP 200
  - PAYMENT-RESPONSE
## 当前实现
- 符合标准
  - HTTP 402状态码
  - 标准headers
  - 链上交易
  - 交易验证
- 可选优化
  - Facilitator（未实现）
  - 批量支付（规划中）
  - 支付订阅（规划中）
## Gas费用
- 当前实现
  - 用户支付（发送）
  - 平台支付（领取）
- 理想状态
  - Facilitator支付
  - 用户仅签名
```

## 协议概述

X402 是一个用于 Web 支付的开放协议，允许客户端通过加密货币支付访问受保护的资源。

## 核心原则

根据 [Coinbase X402 协议](https://github.com/coinbase/x402)：

> **"Easy to use: x402 needs to be 10x better than existing ways to pay on the internet. This means abstracting as many details of crypto as possible away from the client and resource server, and into the facilitator."**

关键点：Gas 费用应该由 Facilitator 处理，客户端和资源服务器不需要考虑 Gas。

## 协议流程

### 1. 客户端请求资源

```
GET /api/resource
```

### 2. 服务器返回 402

```
HTTP/1.1 402 Payment Required
PAYMENT-REQUIRED: {
  "amount": "1000000000000000000",
  "currency": "ETH",
  "chainId": 1,
  "recipient": "0x..."
}
```

### 3. 客户端提供支付证明

```
POST /api/resource
PAYMENT-SIGNATURE: <签名>
```

### 4. 服务器验证支付

- 验证交易哈希
- 验证交易金额
- 验证交易接收者
- 验证链上状态

### 5. 返回资源

```
HTTP/1.1 200 OK
PAYMENT-RESPONSE: {
  "txHash": "0x...",
  "verified": true
}
```

## 当前实现

### 符合 X402 标准

- ✅ 使用 HTTP 402 状态码
- ✅ 使用 PAYMENT-REQUIRED header
- ✅ 使用 PAYMENT-SIGNATURE header
- ✅ 使用 PAYMENT-RESPONSE header
- ✅ 数据结构符合标准
- ✅ 真实的链上交易
- ✅ 交易验证

### 可选优化

- ⚠️ Facilitator（Gas 抽象）：当前未实现，但这是可选的
- ⚠️ 批量支付：规划中
- ⚠️ 支付订阅：规划中

## Gas 费用

### 当前实现

- 用户支付 Gas（发送红包时）
- 平台支付 Gas（领取红包时）

### 理想状态（使用 Facilitator）

- Facilitator 支付 Gas
- 用户只需要签名授权
- 更好的用户体验

## 相关文档

- [红包系统](red-packets.md)
- [X402 Gas 费用说明](https://github.com/Yukitojp/RustChat/blob/main/docs/features/x402-gas-fees-explanation.md)
