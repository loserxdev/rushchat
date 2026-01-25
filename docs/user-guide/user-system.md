# User System

RushChat supports multiple user modes and usage methods.

## User System Overview

```markmap
# User System
## User Modes
- Guest Mode
  - One-click Entry
  - Auto-generated Username
  - View Only
  - Cannot Speak
- Registered User
  - Username & Password
  - Email Optional
  - Invite Code Optional
  - Initial Points
- Login System
  - Password Verification
  - Session Persistence
  - Multi-device Support
## Registration Process
- Fill Information
  - Username (3-20 chars)
  - Password (min 6 chars)
  - Email (optional)
- Optional Invite Code
- Registration Rewards
  - Initial Points
  - Personalized Invite Code
## Login Process
- Enter Credentials
- Password Verification
- Generate Session
- Auto Save
## Reserved Word Protection
- admin
- root
- administrator
- system
- moderator
- Must Password Login
## Session Management
- Auto Recovery
- Refresh Persistence
- Multi-device Login
- Secure Storage
```

## User Modes

### Guest Mode

No registration required, one-click entry to chat room.

**Features**:
- Auto-generated unique username (format: GuestXXXXXX)
- View only, cannot speak or upload images
- Username changes after page refresh

**Usage**:
1. Click "Enter as Guest" button
2. System auto-generates guest username
3. Directly enter chat room

### Registered User

**Registration Requirements**:
- Username: 3-20 characters
- Password: At least 6 characters
- Email: Optional

**Registration Steps**:
1. Click "Register" button
2. Fill in username, password, email (optional)
3. Optional: Enter invite code (if accessed via invitation link)
4. Click "Register"

**Registration Rewards**:
- Initial points
- Personalized invite code

### Login

**Login Steps**:
1. Enter username and password
2. Click "Login"
3. System automatically saves login state

**Session Persistence**:
- Page refresh automatically restores login state
- Supports multi-device login

## Reserved Word Protection

The following usernames must use password login, cannot be used as guest:
- admin
- root
- administrator
- system
- moderator
- mod
- superadmin
- super
- owner
- manager

## Profile

### Set Avatar

1. Click user avatar in top right corner
2. Select "Profile"
3. Click avatar area
4. Select image file (supports JPG, PNG, GIF, max 5MB)
5. System automatically compresses and uploads

### Set Email

1. Enter profile page
2. Enter email address in email field
3. System automatically validates email format
4. Click "Save"

### Set Wallet Address

#### EVM Address (Ethereum, etc.)

1. Enter profile page
2. Enter address in EVM address field (format: 0x...)
3. System automatically validates address format
4. Click "Save"

#### SOL Address (Solana)

1. Enter profile page
2. Enter address in SOL address field (Base58 format)
3. System automatically validates address format
4. Click "Save"

### Change Password

1. Enter profile page
2. Click "Change Password"
3. Enter current password and new password
4. Confirm new password
5. Click "Save"

## User Permissions

### Regular User

- Send messages
- Upload images
- Create channels (requires 100,000 points)
- Upload stickers (up to 10)

### Administrator

- All regular user permissions
- Kick users
- Mute users
- Pin messages
- Upload stickers (up to 100)

### Channel Owner

- All regular user permissions
- Set channel password
- Modify channel information
- Upload stickers (up to 100)

## Points System

### Points Acquisition

- **Registration Reward**: Default points for registered users
- **Build Incentive**: Can claim 1,000 points daily
- **Invitation Reward**: Successfully inviting a registered user gets 10,000 points
- **Channel Contribution**: Users registered through invitation link, inviter gets 5 channel contribution points

### Points Consumption

- **Create Channel**: Costs 50,000 points (Rush executives free)

## Honor Levels

Honor levels are divided into 11 levels (0-10), automatically calculated based on total points.

| Level | Points Range | Level Name |
|-------|-------------|------------|
| Level 0 | 0-99 points | Novice |
| Level 1 | 100-199 points | Beginner |
| Level 2 | 200-299 points | Junior |
| Level 3 | 300-499 points | Intermediate |
| Level 4 | 500-799 points | Advanced |
| Level 5 | 800-1299 points | Senior |
| Level 6 | 1300-1999 points | Expert |
| Level 7 | 2000-2999 points | Master |
| Level 8 | 3000-4999 points | Legend |
| Level 9 | 5000-7999 points | Myth |
| Level 10 | 8000+ points | Legendary |

### Scoring Mechanism

1. **Online Time**: Every 60 minutes online = 1 point
2. **Invitations**: Every successful invitation = 10 points
3. **Message Count**: Every 100 messages sent = 1 point
4. **Message Likes**: Each like = 2 points
5. **Contract Recommendations**: Each contract recommended = 5 points
6. **Recommendation Score**: Average voting score × 10

## Related Documentation

- [Real-time Chat](chat.md)
- [Channel System](channels.md)
- [Profile](profile.md)
