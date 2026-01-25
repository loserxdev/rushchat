# Changelog

> This document records all version updates and feature changes of RushChat.

## Changelog Overview

```markmap
# Changelog
## [Unreleased] - In Development
- New Features
  - Channel System
  - Points System
  - Wallet Verification
  - Rush Executive Privileges
  - Invitation System
  - Sticker System
  - Voice Chat
  - Red Packets
  - X402 Protocol
- Improvements
  - User List Optimization
  - Session Management
  - Wallet Verification Enhancement
  - Avatar Upload Fix
  - Image Compression
  - Solana NFT Optimization
  - RPC Endpoint Optimization
  - Wallet Connection Optimization
  - Error Handling Enhancement
## [v1.0.0]
- Core Features
  - User System
  - Chat Functionality
  - Permission Management
  - Channel System
  - User Profile
  - Interface Design
```

## [Unreleased] - In Development

### New Features

- ✅ **Channel System**: Support for creating and managing private channels
- ✅ **Points System**: User points management and channel creation costs
- ✅ **Wallet Address Verification**: EVM and SOL address format validation
- ✅ **Rush Executive Privileges**: Free channel creation, free access to private channels
- ✅ **Invitation System**: Personalized invitation codes, share to X, QR code sharing
- ✅ **Custom Stickers**: Users can upload GIF stickers (10 for regular users, 100 for admins and channel owners)
- ✅ **Sticker Duplicate Detection**: Uses SHA256 hash to prevent duplicate uploads
- ✅ **Voice Chat Feature**: WebRTC voice calls, supports multiple users, screen sharing, invitations, permission management
- ✅ **Red Packet System**: EVM and Solana chain red packets, supports regular and random red packets
- ✅ **X402 Protocol**: Implementation of Coinbase X402 payment protocol, supports on-chain payment verification
- ✅ **Wallet Verification Enhancement**: Support for Metaplex Core NFT, DAS API, automatic RPC fallback

### Improvements

- ✅ Optimized user list deduplication logic
- ✅ Improved session management to prevent duplicate logins
- ✅ Enhanced real-time feedback for wallet address verification
- ✅ **Fixed Avatar Upload Issue**: Changed avatar field from VARCHAR(500) to LONGTEXT to support storing large base64 image data
- ✅ **Image Compression Feature**: Automatic image compression when uploading avatars to reduce data size
- ✅ Unified file path logic: Ensures consistent file paths for uploads and serving
- ✅ Optimized route order: Ensures specific routes take priority over generic static file serving
- ✅ **Solana NFT Verification Optimization**: Uses getAssetsByOwner (DAS API) to support Metaplex Core NFT
- ✅ **RPC Endpoint Optimization**: Defaults to Helius RPC, automatically detects DAS API support and falls back
- ✅ **Wallet Connection Optimization**: Improved connection and switching logic for Phantom, OKX, and other wallets
- ✅ **Error Handling Enhancement**: Global error handling, suppresses browser extension and wallet-related errors

## [v1.0.0] - 2024-01-XX

### Core Features

#### User System

- ✅ **Guest Mode**: No registration required, one-click entry to chat room
- ✅ **User Registration**: Supports username, password, and email registration
- ✅ **User Login**: Password verification login
- ✅ **Session Persistence**: Automatically restores login state on page refresh
- ✅ **Reserved Word Protection**: Usernames like admin, root must use password login

#### Chat Functionality

- ✅ **Real-time Messaging**: WebSocket-based real-time communication
- ✅ **Text Messages**: Supports plain text message sending
- ✅ **Image Sharing**: Supports image upload and sharing (max 5MB)
- ✅ **Typing Indicator**: Shows users who are typing
- ✅ **Online User List**: Real-time display of online users
- ✅ **Message History**: Automatically loads historical messages

#### Permission Management

- ✅ **Three-level Administrator System**: A-level (Super Admin), B-level (Rush Executive), C-level (Admin)
- ✅ **IP Banning**: Administrators can ban violating IPs (60 minutes)
- ✅ **User Muting**: Administrators can temporarily mute users (15 minutes)
- ✅ **Administrator Appointment**: Senior administrators can appoint junior administrators

#### Channel System

- ✅ **Public Channels**: Default channels accessible to all users
- ✅ **Private Channels**: Channels that require a password to join
- ✅ **Channel Creation**:
  - Regular users: Requires 100,000 points, creation costs 50,000 points
  - Rush executives: Free creation, no points consumed
- ✅ **Channel Management**: Channel owners can set/modify channel passwords
- ✅ **Channel Switching**: Users can switch channels at any time
- ✅ **Message Isolation**: Messages from different channels are isolated from each other

#### User Profile

- ✅ **Profile Management**: Can set avatar, email, wallet address
- ✅ **Avatar Upload**: Supports image upload (max 5MB)
- ✅ **Wallet Address**:
  - EVM addresses (Ethereum, etc.): Format validation
  - SOL addresses (Solana): Format validation
- ✅ **Password Change**: Supports changing login password

#### Interface Design

- ✅ **Slack-style**: Modern chat interface design
- ✅ **Day/Night Mode**: Supports theme switching
- ✅ **Responsive Design**: Adapts to desktop and mobile devices
- ✅ **Multi-language Support**: Chinese/English switching

### Technical Features

#### Frontend

- React 18 + Hooks
- Socket.io Client
- CSS Variables (Theme System)
- React Context (State Management)
- Real-time validation and feedback

#### Backend

- Rust + Axum
- Tokio WebSocket (WebSocket)
- MySQL (Optional, supports in-memory mode)
- bcrypt (Password encryption)
- Session management

### Database

#### Table Structure

- `users`: User table
- `messages`: Message table
- `channels`: Channel table
- `sessions`: Session table
- `banned_ips`: IP ban table
- `muted_users`: Muted users table
- `admin_logs`: Administrator operation log table

### Security Features

- Password encrypted storage (bcrypt)
- Reserved word protection
- IP banning mechanism
- User muting mechanism
- Administrator operation logs

---

**Built with Rust, React, and MySQL ❤️**
