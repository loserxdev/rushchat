# Rush.Moe Documentation

> Native Solana Web3 real-time chat application (EVM compatible)

![Rush.Moe](https://img.shields.io/badge/Rush.Moe-v2.0.0-blue)
![Rust](https://img.shields.io/badge/Rust-1.70+-orange)
![React](https://img.shields.io/badge/React-18-blue)

## 🚀 Introduction

**Rush.Moe** is a native Solana Web3 real-time chat application (EVM compatible). **Discovering Alpha and instant trading opportunities first** is Rush's core philosophy.

Anyone can build their own Alpha channel on Rush.Moe (with options for paid/private channels, earning trading fees, supporting Solana & EVM NFT verification for private channel access). Voice chat further enhances real-time community communication efficiency.

Invite friends to join Rush.Moe and share channel creation fees & trading fees (upcoming feature).

## ✨ Core Features

```markmap
# Rush.Moe Core Features
## Communication
- Real-time Messaging
  - WebSocket
  - Text Messages
  - Image Sharing
- Voice Chat
  - WebRTC
  - Screen Sharing
  - Multi-user Support
  - Enhanced Community Efficiency
## Alpha Channel System
- Build Your Own Alpha Channel
  - Paid Channels
  - Private Channels
  - Earn Trading Fees
- Channel Access Control
  - Solana NFT Verification
  - EVM NFT Verification
  - Password Protected
## User Management
- Guest Mode
- Registration & Login
- Profile Management
  - Avatar
  - Wallet Address
  - Email
## Permission System
- Three-level Admin
  - A-level (Super Admin)
  - B-level (Rush Executive)
  - C-level (Admin)
## Points & Honor
- Points System
  - Channel Creation
  - Invitation Rewards
- Honor Levels (0-10)
## Social Features
- Invitation System
  - Share Channel Creation Fees
  - Share Trading Fees (Upcoming)
- Contract Recommendations
- Sticker System
  - System Emojis
  - Custom GIF Stickers
## Blockchain Integration
- Native Solana Support
- EVM Compatibility
- Wallet Verification
  - EVM Wallets
  - Solana Wallets
- Red Packets
  - EVM Chain
  - Solana Chain
- X402 Protocol
```

## 🎯 Core Philosophy

**Discovering Alpha and instant trading opportunities first** is Rush's core philosophy.

Rush.Moe enables users to:
- Build and manage Alpha channels
- Earn revenue from channel creation and trading fees
- Access exclusive private channels through NFT verification
- Communicate instantly through voice chat

## 🌟 Key Features

### Alpha Channel System

- ✅ **Build Your Own Alpha Channel** - Create paid or private channels
- ✅ **Earn Trading Fees** - Generate revenue from channel activities
- ✅ **NFT Verification** - Solana & EVM NFT verification for private channel access
- ✅ **Flexible Access Control** - Password protection and wallet verification

### Real-time Communication

- 💬 **Real-time Messaging** - WebSocket-based instant messaging
- 🎤 **Voice Chat** - WebRTC voice calls in private channels with screen sharing
- 📱 **Multi-channel Support** - Public and private channels

### Web3 Integration

- 🔗 **Native Solana** - Built for Solana ecosystem
- ⛓️ **EVM Compatible** - Support for Ethereum, BSC, Polygon, etc.
- 🔐 **Wallet Verification** - Connect EVM and Solana wallets
- 💰 **Revenue Sharing** - Share channel creation fees & trading fees (upcoming)

### Social Features

- 👥 **User System** - Guest mode, registration, login, profile management
- 🎁 **Invitation System** - Personalized invitation codes, share to X, QR code sharing
- 📊 **Contract Recommendations** - Users can recommend contracts with multi-emoji voting
- 😊 **Sticker System** - System emojis + user custom GIF stickers

## 🛠️ Tech Stack

### Backend
- **Rust** - Systems programming language
- **Axum** - Async web framework
- **Tokio** - Async runtime
- **SQLx** - Type-safe async SQL toolkit (MySQL)

### Frontend
- **React 18** - UI framework
- **Socket.io Client** - WebSocket communication
- **CSS3** - Modern styling

### Database
- **MySQL 5.7+** - Relational database

## 📚 Documentation Navigation

### Quick Start
- [Installation Guide](installation.md) - How to install and configure Rush.Moe
- [Quick Start](getting-started.md) - Get started in 5 minutes
- [Configuration](configuration.md) - Environment variables and configuration files

### User Guide
- [User System](user-guide/user-system.md) - Registration, login, guest mode
- [Real-time Chat](user-guide/chat.md) - Send messages, images, stickers
- [Channel System](user-guide/channels.md) - Create and join channels
- [Sticker System](user-guide/stickers.md) - Use and manage stickers

### Admin Guide
- [Admin System](admin-guide/admin-system.md) - Three-level administrator system
- [Admin Operations](admin-guide/operations.md) - Kick, mute, appoint

### Technical Documentation
- [Architecture](technical/architecture.md) - System architecture and tech stack
- [API Documentation](technical/api.md) - RESTful API interface documentation
- [WebSocket Events](technical/websocket.md) - WebSocket event list

### Deployment Guide
- [Deployment Overview](deployment/overview.md) - Deployment solutions overview
- [Railway Deployment](deployment/railway.md) - Deploy backend to Railway
- [Vercel Deployment](deployment/vercel.md) - Deploy frontend to Vercel

## 🎯 Quick Start

```bash
# 1. Clone the project
git clone <repository-url>
cd RushChat

# 2. Install dependencies
npm install
cd client && npm install && cd ..

# 3. Create database
mysql -u root -p < database/schema.sql

# 4. Configure environment variables
cp docs/ENVIRONMENT_TEMPLATE.md .env

# 5. Start the application
cd server-rust && cargo run
cd ../client && npm start
```

Visit: `http://localhost:3000`

## 📖 More Information

- [Changelog](changelog.md) - Version update records
- [FAQ](faq.md) - Frequently asked questions
- [Troubleshooting](troubleshooting.md) - Problem troubleshooting guide

## 📄 License

MIT License - Welcome for learning and development.

---

**Built with Rust, React, and MySQL ❤️**
