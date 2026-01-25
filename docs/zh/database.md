# 数据库设计

RushChat 的数据库结构和设计说明。

## 数据库概述

- **数据库类型**: MySQL 5.7+ / MariaDB 10.3+
- **字符集**: utf8mb4（支持 emoji）
- **存储引擎**: InnoDB

## 核心表结构

### users - 用户表

存储用户基本信息和管理员级别。

**主要字段**：
- `id` - 用户 ID（主键）
- `username` - 用户名（唯一）
- `password_hash` - 密码哈希
- `email` - 邮箱（可选）
- `avatar` - 头像（LONGTEXT，base64）
- `points` - 积分
- `admin_level` - 管理员级别（A/B/C/null）
- `honor_level` - 荣誉等级（0-10）
- `evm_address` - EVM 钱包地址
- `sol_address` - Solana 钱包地址
- `created_at` - 创建时间

### messages - 消息表

存储所有聊天消息（文本、图片、系统消息）。

**主要字段**：
- `id` - 消息 ID（主键）
- `channel_id` - 频道 ID（外键）
- `username` - 发送者用户名
- `message` - 消息内容（LONGTEXT）
- `message_type` - 消息类型（text/image/system）
- `is_pinned` - 是否置顶
- `created_at` - 创建时间

### channels - 频道表

存储频道信息（公共/私密频道）。

**主要字段**：
- `id` - 频道 ID（主键）
- `name` - 频道名称（唯一）
- `is_private` - 是否私密频道
- `password_hash` - 密码哈希（私密频道）
- `owner_username` - 房主用户名
- `logo` - 频道 Logo
- `created_at` - 创建时间

### sessions - 在线会话表

存储当前在线用户的会话信息。

**主要字段**：
- `id` - 会话 ID（主键）
- `username` - 用户名
- `socket_id` - WebSocket ID
- `ip_address` - IP 地址
- `channel_id` - 当前频道 ID
- `last_active` - 最后活跃时间

### banned_ips - IP 封禁表

存储被封禁的 IP 地址。

**主要字段**：
- `id` - 记录 ID（主键）
- `ip_address` - IP 地址
- `banned_until` - 封禁到期时间
- `banned_by` - 操作者用户名
- `created_at` - 创建时间

### muted_users - 禁言表

存储被禁言的用户。

**主要字段**：
- `id` - 记录 ID（主键）
- `username` - 用户名
- `muted_until` - 禁言到期时间
- `muted_by` - 操作者用户名
- `created_at` - 创建时间

### admin_logs - 管理员操作日志表

记录所有管理员操作（踢人、禁言、任命等）。

**主要字段**：
- `id` - 日志 ID（主键）
- `admin_username` - 管理员用户名
- `action_type` - 操作类型（kick/mute/appoint）
- `target_username` - 目标用户名
- `details` - 操作详情（JSON）
- `created_at` - 创建时间

## 索引设计

### 主要索引

- `users.username` - 用户名唯一索引
- `messages.channel_id` - 频道 ID 索引
- `messages.created_at` - 时间索引
- `sessions.username` - 用户名索引
- `banned_ips.ip_address` - IP 地址索引

## 数据库维护

### 清理过期数据

可以手动调用存储过程：

```sql
CALL CleanExpiredData();
```

或设置定时任务自动清理。

### 备份数据库

```bash
mysqldump -u root -p rushchat > backup.sql
```

### 恢复数据库

```bash
mysql -u root -p rushchat < backup.sql
```

## 迁移脚本

数据库迁移脚本位于 `database/` 目录：

- `schema.sql` - 基础表结构
- `complete_schema_latest.sql` - 完整最新表结构
- `migration_*.sql` - 增量迁移脚本

## 注意事项

1. 使用 `utf8mb4` 字符集以支持 emoji 和特殊字符
2. 图片数据使用 `LONGTEXT` 类型存储 base64 编码
3. 定期清理过期数据以保持数据库性能
4. 建议定期备份数据库
5. 生产环境建议启用 SSL 连接

## 相关文档

- [数据库 README](https://github.com/Yukitojp/RustChat/blob/main/database/README.md)
- [架构设计](architecture.md)
