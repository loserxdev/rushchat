# API 文档

RushChat 的 RESTful API 接口文档。

## 基础信息

- **Base URL**: `http://localhost:5001/api`
- **Content-Type**: `application/json`
- **认证方式**: Session（通过 WebSocket 或 Cookie）

## 认证相关

### 用户注册

```http
POST /api/auth/register
```

**请求体**：
```json
{
  "username": "string",
  "password": "string",
  "email": "string (optional)",
  "invite_code": "string (optional)"
}
```

**响应**：
```json
{
  "success": true,
  "message": "注册成功",
  "user": {
    "username": "string",
    "points": 0
  }
}
```

### 用户登录

```http
POST /api/auth/login
```

**请求体**：
```json
{
  "username": "string",
  "password": "string"
}
```

**响应**：
```json
{
  "success": true,
  "message": "登录成功",
  "user": {
    "username": "string",
    "admin_level": null
  }
}
```

## 用户相关

### 获取用户信息

```http
GET /api/user/:username
```

**响应**：
```json
{
  "username": "string",
  "email": "string",
  "avatar": "string (base64)",
  "points": 0,
  "admin_level": null,
  "honor_level": 0
}
```

### 更新用户资料

```http
PUT /api/user/:username
```

**请求体**：
```json
{
  "email": "string (optional)",
  "avatar": "string (base64, optional)",
  "evm_address": "string (optional)",
  "sol_address": "string (optional)",
  "password": "string (optional)"
}
```

### 获取用户荣誉信息

```http
GET /api/user/:username/honor
```

**响应**：
```json
{
  "honor_level": 0,
  "total_points": 0,
  "online_hours": 0,
  "invite_count": 0,
  "message_count": 0
}
```

## 频道相关

### 获取频道列表

```http
GET /api/channels
```

**响应**：
```json
{
  "channels": [
    {
      "id": 1,
      "name": "string",
      "is_private": false,
      "owner_username": "string"
    }
  ]
}
```

### 创建频道

```http
POST /api/channels
```

**请求体**：
```json
{
  "name": "string",
  "is_private": true,
  "password": "string (optional)"
}
```

### 更新频道

```http
PUT /api/channels/:channel_id
```

### 删除频道

```http
DELETE /api/channels/:channel_id
```

## 消息相关

### 获取历史消息

```http
GET /api/messages?channel_id=1&limit=50
```

**查询参数**：
- `channel_id`: 频道 ID
- `limit`: 返回数量（默认 50）
- `before`: 在此消息 ID 之前（分页）

### 置顶消息

```http
POST /api/messages/:messageId/pin
```

### 取消置顶

```http
POST /api/messages/:messageId/unpin
```

## 表情包相关

### 上传表情包

```http
POST /api/stickers/upload
```

**请求**：`multipart/form-data`
- `file`: GIF 图片文件
- `sticker_name`: 表情包名称（可选）

### 获取表情包列表

```http
GET /api/stickers?username=xxx
```

### 删除表情包

```http
DELETE /api/stickers/:sticker_id
```

## 红包相关

### 创建红包

```http
POST /api/red-packets
```

### 领取红包

```http
POST /api/red-packets/:packet_id/claim
```

## 错误响应

所有错误响应格式：

```json
{
  "success": false,
  "error": "错误消息"
}
```

## 相关文档

- [WebSocket 事件](websocket.md)
- [架构设计](architecture.md)
