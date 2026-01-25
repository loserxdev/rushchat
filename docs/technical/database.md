# Database Design

RushChat database structure and design documentation.

## Database Design Overview

```markmap
# Database Design
## Database Information
- Type
  - MySQL 5.7+
  - MariaDB 10.3+
- Character Set
  - utf8mb4
  - Supports Emoji
- Storage Engine
  - InnoDB
## Core Tables
- users
  - User Information
  - Points & Honor
  - Admin Level
  - Wallet Address
- messages
  - Message Content
  - Message Type
  - Channel Association
  - Pin Status
- channels
  - Channel Information
  - Private/Public
  - Password & Rules
  - Owner Information
- sessions
  - Online Sessions
  - User Status
  - Connection Management
## Management Tables
- banned_ips
  - IP Ban Records
  - Expiration Time
- muted_users
  - Mute Records
  - Expiration Time
- admin_logs
  - Operation Logs
  - Operation Type
  - Operator Information
## Feature Tables
- user_stickers
  - User Stickers
  - File Hash
- contract_recommendations
  - Contract Recommendations
  - Chain Type
- contract_votes
  - Voting Records
  - Voting Emoji
- user_invitations
  - Invitation Relationships
  - Invite Code
- red_packets
  - Red Packet Records
  - Chain Type
  - Status Management
```

## Database Overview

- **Database Type**: MySQL 5.7+ / MariaDB 10.3+
- **Character Set**: utf8mb4 (supports emoji)
- **Storage Engine**: InnoDB

## Core Table Structure

### users - User Table

Stores user basic information and admin level.

**Main Fields**:
- `id` - User ID (primary key)
- `username` - Username (unique)
- `password_hash` - Password hash
- `email` - Email (optional)
- `avatar` - Avatar (LONGTEXT, base64)
- `points` - Points
- `admin_level` - Admin level (A/B/C/null)
- `honor_level` - Honor level (0-10)
- `evm_address` - EVM wallet address
- `sol_address` - Solana wallet address
- `created_at` - Creation time

### messages - Message Table

Stores all chat messages (text, images, system messages).

**Main Fields**:
- `id` - Message ID (primary key)
- `channel_id` - Channel ID (foreign key)
- `username` - Sender username
- `message` - Message content (LONGTEXT)
- `message_type` - Message type (text/image/system)
- `is_pinned` - Whether pinned
- `created_at` - Creation time

### channels - Channel Table

Stores channel information (public/private channels).

**Main Fields**:
- `id` - Channel ID (primary key)
- `name` - Channel name (unique)
- `is_private` - Whether private channel
- `password_hash` - Password hash (private channel)
- `owner_username` - Owner username
- `logo` - Channel logo
- `created_at` - Creation time

### sessions - Online Session Table

Stores current online user session information.

**Main Fields**:
- `id` - Session ID (primary key)
- `username` - Username
- `socket_id` - WebSocket ID
- `ip_address` - IP address
- `channel_id` - Current channel ID
- `last_active` - Last active time

### banned_ips - IP Ban Table

Stores banned IP addresses.

**Main Fields**:
- `id` - Record ID (primary key)
- `ip_address` - IP address
- `banned_until` - Ban expiration time
- `banned_by` - Operator username
- `created_at` - Creation time

### muted_users - Mute Table

Stores muted users.

**Main Fields**:
- `id` - Record ID (primary key)
- `username` - Username
- `muted_until` - Mute expiration time
- `muted_by` - Operator username
- `created_at` - Creation time

### admin_logs - Admin Operation Log Table

Records all admin operations (kick, mute, appoint, etc.).

**Main Fields**:
- `id` - Log ID (primary key)
- `admin_username` - Admin username
- `action_type` - Operation type (kick/mute/appoint)
- `target_username` - Target username
- `details` - Operation details (JSON)
- `created_at` - Creation time

## Index Design

### Main Indexes

- `users.username` - Username unique index
- `messages.channel_id` - Channel ID index
- `messages.created_at` - Time index
- `sessions.username` - Username index
- `banned_ips.ip_address` - IP address index

## Database Maintenance

### Clean Expired Data

Can manually call stored procedure:

```sql
CALL CleanExpiredData();
```

Or set up scheduled tasks for automatic cleanup.

### Backup Database

```bash
mysqldump -u root -p rushchat > backup.sql
```

### Restore Database

```bash
mysql -u root -p rushchat < backup.sql
```

## Migration Scripts

Database migration scripts are located in `database/` directory:

- `schema.sql` - Basic table structure
- `complete_schema_latest.sql` - Complete latest table structure
- `migration_*.sql` - Incremental migration scripts

## Notes

1. Use `utf8mb4` character set to support emoji and special characters
2. Image data uses `LONGTEXT` type to store base64 encoding
3. Regularly clean expired data to maintain database performance
4. Recommend regular database backups
5. Production environment recommend enabling SSL connections

## Related Documentation

- [Database README](https://github.com/Yukitojp/RustChat/blob/main/database/README.md)
- [Architecture](architecture.md)
