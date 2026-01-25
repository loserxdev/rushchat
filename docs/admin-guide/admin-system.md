# Admin System

RushChat uses a three-level administrator system, with different levels having different management permissions.

## Admin System Overview

```markmap
# Admin System
## A-level: Super Admin
- All Management Permissions
  - Kick Users
  - Mute Users
  - Appoint Admins
  - View Logs
- Operation Scope
  - All Users
  - All Channels
  - Other Admins
## B-level: Rush Executive
- Management Permissions
  - Kick Users
  - Mute Users
  - Appoint C-level Admins
- Special Permissions
  - Free Channel Creation
  - Free Access to Private Channels
  - 100 Stickers
## C-level: Regular Admin
- Basic Permissions
  - Kick Users
  - Mute Users
- Restrictions
  - Cannot Appoint Admins
  - Cannot Create Channels for Free
## Management Operations
- IP Banning
  - 60 Minutes
  - Auto Release
- User Muting
  - 15 Minutes
  - Temporary Restriction
- Message Pinning
  - Important Notices
  - Channel Announcements
## Operation Logs
- Record All Operations
- Operator Tracking
- Timestamp Records
```

## Admin Levels

### A-level: Super Admin

Highest level administrator with all management permissions.

**Permissions**:
- ✅ Kick users
- ✅ Mute users
- ✅ Appoint B-level and C-level admins
- ✅ View operation logs
- ✅ Operate all levels of users (including other admins)
- ✅ All channel management permissions

### B-level: Rush Executive

Senior administrator with most management permissions.

**Permissions**:
- ✅ Kick users
- ✅ Mute users
- ✅ Appoint C-level admins
- ✅ **Free channel creation** (no points consumed)
- ✅ **Free access to private channels** (no password required)
- ✅ Upload stickers (up to 100)

**Restrictions**:
- ❌ Cannot appoint B-level admins
- ❌ Cannot operate A-level admins

### C-level: Regular Admin

Basic administrator with fundamental management permissions.

**Permissions**:
- ✅ Kick users
- ✅ Mute users
- ✅ Pin messages
- ✅ Upload stickers (up to 100)

**Restrictions**:
- ❌ Cannot appoint other admins
- ❌ Cannot operate other admins

## Admin Appointment

### A-level Appoints B-level or C-level

1. Open admin panel
2. Find target user
3. Click "Appoint Admin"
4. Select admin level (B-level or C-level)
5. Confirm operation

### B-level Appoints C-level

1. Open admin panel
2. Find target user
3. Click "Appoint Admin"
4. Select C-level
5. Confirm operation

## Admin Badges

Admins have special badges in the chat interface:

- Admin badge displayed next to username
- Different levels display different colors
- Level information displayed in admin panel

## Operation Logs

All admin operations are recorded:

- Operation type (kick, mute, appoint, etc.)
- Operation target
- Operation time
- Operator information

A-level admins can view complete operation logs.

## Related Documentation

- [Admin Operations](operations.md)
- [Permissions](permissions.md)
