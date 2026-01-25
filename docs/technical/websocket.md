# WebSocket Events

RushChat uses WebSocket for real-time communication.

## WebSocket Events Overview

```markmap
# WebSocket Event System
## Connection
- Connection Address
  - ws://localhost:5001/ws
  - wss://domain.com/ws
- Connection Method
  - Auto Connect
  - Auto Reconnect
## Client → Server
- User Events
  - user:join
  - user:login
- Message Events
  - message:send
  - typing:start
  - typing:stop
- Channel Events
  - channel:join
  - channel:create
- Admin Events
  - admin:kick
  - admin:mute
  - admin:appoint
- Voice Chat
  - voice:join
  - voice:leave
  - voice:signal
  - voice:mute
  - voice:kick
  - voice:invite
## Server → Client
- User Notifications
  - user:joined
  - user:left
  - user:list
- Message Notifications
  - message:receive
  - typing:start
  - typing:stop
- Channel Notifications
  - channel:joined
  - channel:list
- Admin Notifications
  - admin:action
  - admin:info
- Error Notifications
  - error
```

## Connection

### Connection Address

```
ws://localhost:5001/ws
```

Or using HTTPS:

```
wss://your-domain.com/ws
```

## Client → Server Events

### user:join

User joins chat.

```json
{
  "event": "user:join",
  "data": {
    "username": "string"
  }
}
```

### user:login

User login.

```json
{
  "event": "user:login",
  "data": {
    "username": "string",
    "password": "string"
  }
}
```

### message:send

Send message.

```json
{
  "event": "message:send",
  "data": {
    "channel_id": 1,
    "message": "string",
    "message_type": "text|image|system"
  }
}
```

### typing:start

User starts typing.

```json
{
  "event": "typing:start",
  "data": {
    "channel_id": 1
  }
}
```

### typing:stop

User stops typing.

```json
{
  "event": "typing:stop",
  "data": {
    "channel_id": 1
  }
}
```

### channel:join

Join channel.

```json
{
  "event": "channel:join",
  "data": {
    "channel_id": 1,
    "password": "string (optional)"
  }
}
```

### channel:create

Create channel.

```json
{
  "event": "channel:create",
  "data": {
    "name": "string",
    "is_private": true,
    "password": "string (optional)"
  }
}
```

### admin:kick

Admin kicks user.

```json
{
  "event": "admin:kick",
  "data": {
    "target_username": "string"
  }
}
```

### admin:mute

Admin mutes user.

```json
{
  "event": "admin:mute",
  "data": {
    "target_username": "string"
  }
}
```

### admin:appoint

Admin appointment.

```json
{
  "event": "admin:appoint",
  "data": {
    "target_username": "string",
    "admin_level": "A|B|C"
  }
}
```

## Server → Client Events

### user:joined

Notify user joined.

```json
{
  "event": "user:joined",
  "data": {
    "username": "string"
  }
}
```

### user:left

Notify user left.

```json
{
  "event": "user:left",
  "data": {
    "username": "string"
  }
}
```

### user:list

Send online user list.

```json
{
  "event": "user:list",
  "data": {
    "users": ["username1", "username2"]
  }
}
```

### message:receive

Receive new message.

```json
{
  "event": "message:receive",
  "data": {
    "id": 1,
    "channel_id": 1,
    "username": "string",
    "message": "string",
    "message_type": "text|image|system",
    "created_at": "2024-01-01T00:00:00Z"
  }
}
```

### typing:start

Someone is typing.

```json
{
  "event": "typing:start",
  "data": {
    "username": "string",
    "channel_id": 1
  }
}
```

### typing:stop

Someone stopped typing.

```json
{
  "event": "typing:stop",
  "data": {
    "username": "string",
    "channel_id": 1
  }
}
```

### channel:joined

Join channel successful.

```json
{
  "event": "channel:joined",
  "data": {
    "channel_id": 1,
    "channel_name": "string"
  }
}
```

### channel:list

Channel list updated.

```json
{
  "event": "channel:list",
  "data": {
    "channels": [
      {
        "id": 1,
        "name": "string",
        "is_private": false
      }
    ]
  }
}
```

### admin:action

Admin operation notification.

```json
{
  "event": "admin:action",
  "data": {
    "action_type": "kick|mute|appoint",
    "admin_username": "string",
    "target_username": "string"
  }
}
```

### error

Error message.

```json
{
  "event": "error",
  "data": {
    "message": "string"
  }
}
```

## Connection Management

### Auto Reconnect

Client automatically handles disconnection and reconnection:

- Detect disconnection
- Automatically attempt reconnection
- Restore session after reconnection

### Heartbeat

Server periodically sends heartbeat packets to keep connection alive.

## Related Documentation

- [API Documentation](api.md)
- [Architecture](architecture.md)
