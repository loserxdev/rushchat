# React Frontend

RushChat's frontend is built with React 18.

## React Frontend Overview

```markmap
# React Frontend
## Technology Stack
- React 18
  - UI Framework
  - Hooks
  - Context
- Socket.io Client
  - WebSocket Communication
  - Real-time Connection
- CSS Variables
  - Theme System
  - Day/Night Mode
- Wagmi
  - Ethereum Wallet
  - Connection Management
- Viem
  - Ethereum Utilities
  - Transaction Processing
## Project Structure
- components/
  - ChatRoom
  - ChannelManager
  - MessageList
  - WalletConnect
- utils/
  - websocket.js
  - wallet.js
- i18n/
  - Chinese/English Switch
  - Internationalization Support
- config/
  - wagmi.js
## Core Components
- ChatRoom
  - Message List
  - Message Input
  - User List
- ChannelManager
  - Channel List
  - Channel Creation
  - Channel Switching
- WalletConnect
  - Wallet Connection
  - Address Management
- MessageList
  - Message Display
  - History Loading
```

## Technology Stack

- **React 18** - UI framework
- **Socket.io Client** - WebSocket communication
- **CSS Variables** - Theme system
- **React Context** - State management
- **Wagmi** - Ethereum wallet connection
- **Viem** - Ethereum utilities

## Project Structure

```
client/
├── src/
│   ├── App.js               # Main application component
│   ├── index.js             # Entry point
│   ├── components/          # React components
│   │   ├── ChatRoom.js
│   │   ├── ChannelManager.js
│   │   ├── MessageList.js
│   │   └── ...
│   ├── utils/               # Utility functions
│   │   ├── websocket.js
│   │   ├── wallet.js
│   │   └── ...
│   ├── i18n/                # Internationalization
│   │   ├── index.js
│   │   └── locales/
│   │       ├── zh.js
│   │       └── en.js
│   └── config/              # Configuration files
│       └── wagmi.js
├── public/                  # Static files
└── package.json
```

## Core Components

### ChatRoom

Main chat room component, includes:

- Message list
- Message input
- User list
- Emoji selector

### ChannelManager

Channel management component, includes:

- Channel list
- Channel creation
- Channel switching

### WalletConnect

Wallet connection component, supports:

- MetaMask
- OKX Wallet
- Phantom
- Coinbase Wallet
- Other EVM and Solana wallets

## Features

### Real-time Communication

- WebSocket connection
- Auto reconnect
- Real-time message updates

### Theme System

- Day/night mode
- CSS Variables
- Smooth transition animations

### Internationalization

- Supports Chinese and English
- Uses i18next
- Dynamic language switching

### Responsive Design

- Mobile adaptation
- Desktop optimization
- Adaptive layout

## Development

### Install Dependencies

```bash
cd client
npm install
```

### Start Development Server

```bash
npm start
```

### Build Production Version

```bash
npm run build
```

## Related Documentation

- [Architecture](architecture.md)
- [API Documentation](api.md)
