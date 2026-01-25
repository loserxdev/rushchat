# Admin Operations

Administrator operations that can be performed.

## Admin Operations Overview

```markmap
# Admin Operations
## Kick User
- Operation Steps
  - Open Admin Panel
  - Find Target User
  - Click Kick Button
  - Confirm Operation
- Effects
  - Immediate Disconnect
  - IP Ban 60 Minutes
  - Record Operation Log
- Permission Limits
  - A-level: Can Kick All Users
  - B-level: Cannot Kick A-level
  - C-level: Can Only Kick Regular Users
## Mute User
- Operation Steps
  - Open Admin Panel
  - Find Target User
  - Click Mute Button
  - Confirm Operation
- Effects
  - Cannot Speak for 15 Minutes
  - Messages Not Displayed
  - Record Operation Log
- Notes
  - Fixed 15 Minutes
  - Can Repeat Mute
  - Does Not Affect Viewing
## Appoint Admin
- Operation Steps
  - Open Admin Panel
  - Find Target User
  - Select Admin Level
  - Confirm Operation
- Permission Requirements
  - A-level: Can Appoint B-level and C-level
  - B-level: Can Only Appoint C-level
  - C-level: Cannot Appoint
- Revoke Appointment
  - Only A-level Can Revoke
  - Restore to Regular User
## Pin Message
- Operation Steps
  - Find Message
  - Click Message Menu
  - Select Pin
- Effects
  - Display at Channel Top
  - All Users Visible
  - Can Unpin
- Permissions
  - All Admins
  - Channel Owner
## Operation Logs
- View Permission
  - Only A-level Admins
- Log Content
  - Operation Type
  - Operation Target
  - Operation Time
  - Operator Information
```

## Kick User

### Operation Steps

1. Open admin panel
2. Find target user
3. Click "Kick" button
4. Confirm operation

### Effects

- User immediately disconnected
- Same IP address cannot enter for 60 minutes
- Operation recorded in logs

### Notes

- Can only kick regular users and lower-level admins
- A-level admins can kick all users
- B-level admins cannot kick A-level admins
- C-level admins cannot kick other admins

## Mute User

### Operation Steps

1. Open admin panel
2. Find target user
3. Click "Mute" button
4. Confirm operation

### Effects

- User cannot speak for 15 minutes
- Can send messages but they won't be displayed
- Operation recorded in logs

### Notes

- Mute duration is fixed at 15 minutes
- Can repeat mute to extend mute duration
- Muting does not affect user viewing messages

## Appoint Admin

### Operation Steps

1. Open admin panel
2. Find target user
3. Click "Appoint Admin" button
4. Select admin level
5. Confirm operation

### Permission Requirements

- **A-level Admin**: Can appoint B-level and C-level
- **B-level Admin**: Can only appoint C-level
- **C-level Admin**: Cannot appoint other admins

### Revoke Appointment

- Only A-level admins can revoke other admins' appointments
- After revocation, user is restored to regular user

## Pin Message

### Operation Steps

1. Find message to pin
2. Click message menu
3. Select "Pin"
4. Confirm operation

### Effects

- Message displayed at channel top
- All users can see it
- Can unpin

### Permissions

- All admins can pin messages
- Channel owners can also pin messages

## View Operation Logs

### A-level Admin

1. Open admin panel
2. Click "Operation Logs"
3. View all admin operation records

### Log Content

- Operation type
- Operation target
- Operation time
- Operator information
- Operation details

## Related Documentation

- [Admin System](admin-system.md)
- [Permissions](permissions.md)
