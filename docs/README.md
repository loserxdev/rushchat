# RushChat Documentation

> Real-time chat application built with Rust backend and React frontend

![RushChat](https://img.shields.io/badge/RushChat-v2.0.0-blue)
![Rust](https://img.shields.io/badge/Rust-1.70+-orange)
![React](https://img.shields.io/badge/React-18-blue)

## 🚀 Introduction

RushChat is a modern real-time chat application built with Rust backend and React frontend, supporting multiple channels, real-time messaging, stickers, contract recommendations, and more.

## ✨ Core Features

```markmap
# RushChat Core Features
## Communication
- Real-time Messaging
  - WebSocket
  - Text Messages
  - Image Sharing
- Voice Chat
  - WebRTC
  - Screen Sharing
  - Multi-user Support
## Channel System
- Public Channels
- Private Channels
  - Password Protected
  - Wallet Verification
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
- Contract Recommendations
- Sticker System
  - System Emojis
  - Custom GIF Stickers
## Blockchain Integration
- Wallet Verification
  - EVM Wallets
  - Solana Wallets
- Red Packets
  - EVM Chain
  - Solana Chain
- X402 Protocol
```

- 💬 **Real-time Communication** - WebSocket-based instant messaging
- 📱 **Multi-channel Support** - Public and private channels
- 👥 **User System** - Guest mode, registration, login, profile management
- 🔐 **Permission Management** - Three-level administrator system
- 💰 **Points System** - User points management and channel creation costs
- 🏆 **Honor Levels** - 0-10 level honor system
- 🎁 **Invitation System** - Personalized invitation codes, share to X, QR code sharing
- 📊 **Contract Recommendations** - Users can recommend contracts with multi-emoji voting
- 😊 **Sticker System** - System emojis + user custom GIF stickers
- 🎤 **Voice Chat** - WebRTC voice calls in private channels with screen sharing

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
- [Installation Guide](installation.md) - How to install and configure RushChat
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
