# FAQ

## FAQ Overview

```markmap
# FAQ
## Installation & Configuration
- How to Install
  - Check Installation Guide
  - System Requirements
  - Installation Steps
- Database Connection Failed
  - Check MySQL Running
  - Check .env Configuration
  - Verify Database Exists
- Port Occupied
  - Change PORT
  - Update Configuration
  - Stop Process
- CORS Error
  - Check CLIENT_URL
  - Ensure HTTPS
  - Check Domain
## Usage Questions
- How to Register
  - Click Register
  - Fill Information
  - Confirm Registration
- How to Create Channel
  - Click + Button
  - Enter Name
  - Select Type
  - Points Required
- How to Connect Wallet
  - Click Connect
  - Select Wallet
  - Confirm Connection
## Feature Questions
- Points Acquisition
  - Registration Reward
  - Build Incentive
  - Invitation Reward
- Honor Levels
  - Auto Calculation
  - Points Accumulation
  - Level Up
```

## Installation & Configuration

### Q: How to install RushChat?

A: Please check the [Installation Guide](installation.md) for detailed installation steps.

### Q: What to do if database connection fails?

A: Check the following:
- Ensure MySQL is running
- Check database credentials in `.env` file
- Verify database exists: `mysql -u root -p -e "SHOW DATABASES;"`
- Check database user permissions

### Q: What to do if port is already in use?

A:
- Change `PORT` in `.env` file
- Update `REACT_APP_SOCKET_URL` in client
- Or stop the process using the port

### Q: How to resolve CORS errors?

A:
- Check backend `CLIENT_URL` environment variable
- Ensure frontend address includes protocol (`http://` or `https://`)
- Ensure production environment uses HTTPS

## Usage Questions

### Q: How to register an account?

A:
1. Click the "Register" button
2. Fill in username (3-20 characters), password (at least 6 characters), email (optional)
3. Click "Register"

### Q: How to create a channel?

A:
1. Click the "+" button in the left channel list
2. Enter channel name
3. Select "Public Channel" or "Private Channel"
4. If private channel, set password
5. Click "Create"

**Note**:
- Regular users need 100,000 points, creation costs 50,000 points
- Rush executives create for free, no points consumed

### Q: How to upload stickers?

A:
1. Click the emoji icon on the right side of the input box
2. Select "My Stickers" tab
3. Click "Upload Sticker"
4. Select GIF file (max 5MB)

**Limits**:
- Regular users: up to 10
- Admins and channel owners: up to 100

### Q: How to invite friends?

A:
1. Click the user avatar in the top right corner
2. Select "Invite"
3. Copy invitation link or generate QR code
4. Share with friends

**Rewards**:
- Successfully inviting a registered user, inviter gets 10,000 points and 5 channel contribution points

## Feature Questions

### Q: What is guest mode?

A: Guest mode allows users to enter the chat room without registration, but can only view, cannot speak or upload images.

### Q: What is reserved word protection?

A: The following usernames must use password login, cannot be used as guest:
- admin, root, administrator, system, moderator, mod, superadmin, super, owner, manager

### Q: How to become an administrator?

A: Administrators are appointed by senior administrators, cannot apply on their own.

### Q: How to get points?

A:
- Registration reward
- Build incentive (can claim 1,000 points daily)
- Invitation reward (successfully inviting a registered user gets 10,000 points)
- Channel contribution (users registered through invitation link, inviter gets 5 channel contribution points)

### Q: How is honor level calculated?

A: Honor level is automatically calculated based on total points, scoring mechanism includes:
- Online time: Every 60 minutes online = 1 point
- Invitations: Every successful invitation = 10 points
- Message count: Every 100 messages sent = 1 point
- Message likes: Each like = 2 points
- Contract recommendations: Each contract recommended = 5 points
- Recommendation score: Average voting score × 10

## Technical Questions

### Q: What to do if WebSocket connection fails?

A:
- Check if frontend `REACT_APP_SOCKET_URL` is correct
- Ensure using HTTPS address (`https://`)
- WebSocket will automatically convert to `wss://`
- Check if backend service is running normally

### Q: What to do if file upload fails?

A:
- Railway uses temporary file system, will be lost after restart
- Configure Railway Volume for persistent storage
- Or use external storage service (S3, Cloudinary, etc.)

### Q: How to view logs?

A:
- Backend logs: Check terminal output or log files
- Frontend logs: Open browser developer tools (F12)

## Deployment Questions

### Q: How to deploy to production environment?

A: Please check the [Deployment Guide](deployment/overview.md)

### Q: What to note for Railway deployment?

A:
- Configure environment variables
- Set up MySQL database
- Configure Railway Volume for persistent storage
- Set health check endpoint

### Q: What to note for Vercel deployment?

A:
- Configure Root Directory: `client`
- Configure environment variables
- Ensure build command is correct

## Other Questions

### Q: How to report bugs?

A: Please submit an Issue in the GitHub repository, including:
- Problem description
- Reproduction steps
- Expected behavior
- Actual behavior
- Environment information

### Q: How to contribute code?

A: Please check the [Contributing Guide](development/contributing.md)

### Q: How to get help?

A:
- Check [Full Documentation](README.md)
- Check [Troubleshooting](troubleshooting.md)
- Submit GitHub Issue

---

**Need more help?** Please check [Full Documentation](README.md) or submit an Issue.
