# WebSocket 事件

RushChat 使用 WebSocket 实现实时通信。

## 连接

### 连接地址

```
ws://localhost:5001/ws
```

或使用 HTTPS：

```
wss://your-domain.com/ws
```

## 客户端 → 服务器事件

### user:join

用户加入聊天。

```json
{
  "event": "user:join",
  "data": {
    "username": "string"
  }
}
```

### user:login

用户登录。

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

发送消息。

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

用户开始输入。

```json
{
  "event": "typing:start",
  "data": {
    "channel_id": 1
  }
}
```

### typing:stop

用户停止输入。

```json
{
  "event": "typing:stop",
  "data": {
    "channel_id": 1
  }
}
```

### channel:join

加入频道。

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

创建频道。

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

管理员踢人。

```json
{
  "event": "admin:kick",
  "data": {
    "target_username": "string"
  }
}
```

### admin:mute

管理员禁言。

```json
{
  "event": "admin:mute",
  "data": {
    "target_username": "string"
  }
}
```

### admin:appoint

管理员任命。

```json
{
  "event": "admin:appoint",
  "data": {
    "target_username": "string",
    "admin_level": "A|B|C"
  }
}
```

## 服务器 → 客户端事件

### user:joined

通知用户加入。

```json
{
  "event": "user:joined",
  "data": {
    "username": "string"
  }
}
```

### user:left

通知用户离开。

```json
{
  "event": "user:left",
  "data": {
    "username": "string"
  }
}
```

### user:list

发送在线用户列表。

```json
{
  "event": "user:list",
  "data": {
    "users": ["username1", "username2"]
  }
}
```

### message:receive

接收新消息。

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

有人正在输入。

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

有人停止输入。

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

加入频道成功。

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

频道列表更新。

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

管理员操作通知。

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

错误消息。

```json
{
  "event": "error",
  "data": {
    "message": "string"
  }
}
```

## 连接管理

### 自动重连

客户端会自动处理连接断开和重连：

- 检测连接断开
- 自动尝试重连
- 重连后恢复会话

### 心跳检测

服务器会定期发送心跳包，保持连接活跃。

## 相关文档

- [API 文档](api.md)
- [架构设计](architecture.md)
