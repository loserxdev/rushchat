# Permissions

Detailed administrator permission comparison and explanation.

## Permission System Overview

```markmap
# Administrator Permission System
## A-level: Super Admin
- User Management
  - Kick All Users
  - Mute All Users
  - Operate Other Admins
- Admin Appointment
  - Appoint B-level Admins
  - Appoint C-level Admins
  - Revoke Appointment
- System Management
  - View Operation Logs
  - All Channel Permissions
- Special Permissions
  - Free Channel Creation
  - Free Access to Private Channels
  - 100 Stickers
## B-level: Rush Executive
- User Management
  - Kick Regular Users and C-level
  - Mute Users
  - Cannot Operate A-level
- Admin Appointment
  - Appoint C-level Admins
  - Cannot Appoint B-level
- Special Permissions
  - Free Channel Creation
  - Free Access to Private Channels
  - 100 Stickers
## C-level: Regular Admin
- User Management
  - Kick Regular Users
  - Mute Users
  - Cannot Operate Admins
- Restrictions
  - Cannot Appoint Admins
  - Cannot Create Channels for Free
  - Need Password for Private Channels
- Basic Permissions
  - Pin Messages
  - 100 Stickers
## Permission Inheritance
- A-level Has All Permissions
- B-level Has C-level Permissions + Extra
- C-level Has Basic Management Permissions
## Permission Limits
- Cannot Operate Superiors
- Cannot Appoint Peers or Superiors
```

## Permission Comparison Table

| Feature | A-level (Super Admin) | B-level (Rush Executive) | C-level (Regular Admin) | Regular User |
|---------|----------------------|-------------------------|------------------------|--------------|
| Kick User | ✅ | ✅ | ✅ | ❌ |
| Mute User | ✅ | ✅ | ✅ | ❌ |
| Appoint B-level Admin | ✅ | ❌ | ❌ | ❌ |
| Appoint C-level Admin | ✅ | ✅ | ❌ | ❌ |
| View Operation Logs | ✅ | ❌ | ❌ | ❌ |
| Operate Other Admins | ✅ | ❌ | ❌ | ❌ |
| Free Channel Creation | ✅ | ✅ | ❌ | ❌ |
| Free Access to Private Channels | ✅ | ✅ | ❌ | ❌ |
| Pin Message | ✅ | ✅ | ✅ | ❌ |
| Upload Stickers (100) | ✅ | ✅ | ✅ | ❌ (10) |

## Detailed Permission Explanation

### User Management Permissions

#### Kick User

- **A-level**: Can kick all users, including other admins
- **B-level**: Can kick regular users and C-level admins
- **C-level**: Can only kick regular users

#### Mute User

- All admins can mute users
- Mute duration is fixed at 15 minutes
- Can repeat mute to extend mute duration

### Admin Appointment Permissions

#### Appoint B-level Admin

- Only A-level admins can appoint B-level admins
- Need to be cautious, ensure appointee is trustworthy

#### Appoint C-level Admin

- Both A-level and B-level admins can appoint C-level admins
- No limit on number of C-level admins

### Channel Management Permissions

#### Free Channel Creation

- A-level and B-level admins can create channels for free
- No points consumed
- Can create public and private channels

#### Free Access to Private Channels

- A-level and B-level admins can freely access private channels
- No password required
- Convenient for management and supervision

### Content Management Permissions

#### Pin Message

- All admins can pin messages
- Channel owners can also pin messages
- Used to highlight important information

### System Management Permissions

#### View Operation Logs

- Only A-level admins can view complete operation logs
- Used for auditing and tracking
- Ensures system security

## Permission Inheritance

Admin permissions are inherited:

- A-level has all permissions
- B-level has all C-level permissions plus additional permissions
- C-level has basic management permissions

## Permission Limits

### Cannot Operate Superiors

- B-level cannot operate A-level
- C-level cannot operate A-level and B-level

### Cannot Appoint Peers or Superiors

- B-level cannot appoint B-level
- C-level cannot appoint any admins

## Related Documentation

- [Admin System](admin-system.md)
- [Admin Operations](operations.md)
