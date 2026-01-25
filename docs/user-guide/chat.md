# Real-time Chat

Real-time chat functionality in RushChat.

## Real-time Chat Overview

```markmap
# Real-time Chat System
## Message Types
- Text Messages
  - Plain Text
  - Real-time Send
  - Enter to Send
- Image Messages
  - JPG/PNG/GIF
  - Max 5MB
  - Auto Upload
- Emoji Messages
  - System Emojis
  - Custom GIF
  - Emoji Categories
## Message Features
- Typing Indicator
  - Real-time Display
  - Typing Notification
- Online User List
  - Right Side Display
  - Real-time Update
- Message History
  - Auto Load
  - Scroll View
  - Time Display
- Message Pinning
  - Admin Operation
  - Important Notices
## Send Process
- Enter Message
- Select Type
  - Text
  - Image
  - Emoji
- Send Confirmation
- WebSocket Transfer
- Real-time Display
## Interactive Features
- Message Likes
- Message Reply (Planned)
- Message Forward (Planned)
```

## Sending Messages

### Send Text Message

1. Enter message in input box
2. Press `Enter` or click "Send" button
3. Message is immediately sent to current channel

### Send Image

1. Click image icon on the right side of input box
2. Select image file (max 5MB)
3. System automatically uploads and sends
4. Supported formats: JPG, PNG, GIF

### Send Emoji

1. Click emoji icon on the right side of input box
2. Select emoji category
3. Click emoji to send

### Send Custom Sticker

1. Click emoji icon on the right side of input box
2. Select "My Stickers" tab
3. Click sticker to send
4. Can upload new GIF stickers

## Message Features

### Typing Indicator

When other users are typing, a "typing..." notification is displayed in the chat interface.

### Online User List

The right side displays the online user list for the current channel, updated in real-time.

### Message History

- Automatically loads historical messages
- Supports scrolling to view
- Displays message send time and sender

### Message Pinning

Administrators can pin important messages, pinned messages are displayed at the top of the channel.

## Message Types

### Text Message

Plain text messages, supports Markdown format (planned).

### Image Message

Uploaded images are displayed as messages, supports clicking to view full size.

### System Message

System auto-generated messages, such as user join/leave, channel creation, etc.

### Contract Recommendation Message

Contract addresses recommended by users, supports voting and comments.

## Related Documentation

- [User System](user-system.md)
- [Channel System](channels.md)
- [Sticker System](stickers.md)
