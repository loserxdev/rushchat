# Voice Chat

RushChat supports WebRTC voice calls in private channels.

## Feature Overview

Voice chat allows users to make real-time voice calls in private channels, supporting multiple users online simultaneously, screen sharing, and more.

## Voice Chat Overview

```markmap
# Voice Chat System
## Core Features
- Multi-user Voice Calls
  - No User Limit
  - Real-time Audio
  - Low Latency
- Screen Sharing
  - Real-time Sharing
  - Status Notification
  - Multi-user Viewing
## Permission Management
- Voice Chat Owner
  - Independent Permissions
  - Auto Transfer
  - Channel Owner Takeover
- Management Operations
  - Mute Members
  - Kick Members
  - Invite Users
## Invitation System
- Owner Invitation
- Accept/Reject
- Notification Mechanism
## Technical Implementation
- WebRTC
  - Peer-to-peer Communication
  - NAT Traversal
  - High Quality Audio
- Signaling Server
  - WebSocket
  - SDP Exchange
  - ICE Candidates
- State Management
  - Participant List
  - Owner Management
  - Auto Sync
```

## Features

### Multi-user Voice Calls

- ✅ Supports multiple users online simultaneously (no fixed limit)
- ✅ Real-time audio transmission
- ✅ Low latency communication
- ✅ WebRTC peer-to-peer communication

### Voice Controls

- ✅ Mute/Unmute
- ✅ Volume control
- ✅ Microphone switch
- ✅ Owner can mute other members
- ✅ Owner can kick members

### Screen Sharing

- ✅ Supports screen sharing
- ✅ Real-time sharing status notification
- ✅ Other members can see sharing status

### Permission Management

- ✅ Voice chat owner permissions (independent from channel owner)
- ✅ Channel owner automatically takes over voice chat owner permissions
- ✅ Owner can mute specific users
- ✅ Owner can kick voice room members
- ✅ Owner can invite other users to join voice chat
- ✅ Permissions automatically transfer when owner leaves

### Invitation Feature

- ✅ Voice chat owner can invite other users
- ✅ Invited users receive notifications
- ✅ Supports accept/reject invitation

## Usage

### Join Voice Room

1. Enter private channel
2. Click "Join Voice" button
3. Allow browser to access microphone
4. Automatically join voice room
5. System notifies other members in channel

### Leave Voice Room

1. Click "Leave Voice" button
2. Or close channel page
3. Automatically disconnect
4. If user is voice chat owner, permissions automatically transfer to other participants

### Invite Other Users

1. As voice chat owner, click "Invite" button
2. Select user to invite
3. Invited user receives notification
4. Invited user can choose to accept or reject

### Manage Voice Room

1. **Mute Members**: Owner can click mute button in member list
2. **Kick Members**: Owner can kick inactive or violating members
3. **View Status**: Can view current voice chat participant list

## Technical Implementation

### WebRTC

Uses WebRTC technology for peer-to-peer communication:

- ✅ Low latency audio transmission
- ✅ High quality audio codec
- ✅ Peer-to-peer direct connection (reduces server load)
- ✅ Automatic NAT traversal

### Signaling Server

Uses WebSocket as signaling server:

- ✅ Establish WebRTC connections
- ✅ Exchange SDP (Session Description Protocol)
- ✅ Exchange ICE candidates (NAT traversal)
- ✅ Real-time state synchronization
- ✅ Signaling data forwarding

### State Management

- ✅ Active voice chat records
- ✅ Participant list management
- ✅ Voice chat owner management
- ✅ Automatic permission transfer
- ✅ Status query interface

### Event System

Supports the following WebSocket events:

- `voice:join` - Join voice chat
- `voice:leave` - Leave voice chat
- `voice:signal` - WebRTC signaling forwarding
- `voice:mute` - Mute operation
- `voice:kick` - Kick operation
- `voice:invite` - Invite to join
- `voice:invite_reject` - Reject invitation
- `voice:screen_share` - Screen sharing status
- `voice:status` - Query voice chat status

## Related Documentation

- [Channel System](../user-guide/channels.md)
- [Technical Architecture](../technical/architecture.md)
