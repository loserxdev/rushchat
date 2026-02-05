# Contract Recommendations

Users can recommend contract addresses in chat, other users can vote and comment.

## Contract Recommendation System Overview

```markmap
# Contract Recommendation System
## Recommend Contract
- Supported Chains
  - EVM Chains
    - Ethereum
    - BSC
    - Polygon
  - Solana Chain
    - Solana Mainnet
- Recommendation Method
  - Enter Address
  - Auto Recognition
  - Display Card
## Voting System
- 7 Emojis
  - 👍 Support
  - 👎 Oppose
  - 🌹 Like
  - 💩 Bad
  - 🥚 Neutral
  - 🤮 Dislike
  - 💎 Recommend
- Voting Features
  - Click to Vote
  - Real-time Statistics
  - Can Change
- Voting Statistics
  - Each Emoji Count
  - Total Votes
  - Average Rating
## Comment Feature
- Add Comment
- View Comments
- Comment Interaction
## Inline Voting
- Display in Chat
- Direct Voting
- Real-time Update
```

## Recommend Contract

### How to Recommend

1. Enter contract address in chat
2. System automatically recognizes and displays as contract recommendation card
3. Other users can see and vote

### Supported Chains

- **EVM Chains**: Ethereum, BSC, Polygon, etc.
- **Solana**: Solana mainnet

### Contract Address Format

- **EVM**: `0x` prefixed 42-character address
- **Solana**: Base58 encoded address (32-44 characters)

## Voting System

### Voting Emojis

Supports 7 emoji votes:

- 👍 Support
- 👎 Oppose
- 🌹 Like
- 💩 Bad
- 🥚 Neutral
- 🤮 Dislike
- 💎 Recommend

### How to Vote

1. Click contract recommendation card
2. Select voting emoji
3. Confirm vote
4. Can change vote at any time

### Voting Statistics

- Real-time display of each emoji's vote count
- Display total votes
- Display average rating

## Comment Feature

### Add Comment

1. Click contract recommendation card
2. Scroll to comment area
3. Enter comment content
4. Click "Send"

### View Comments

- All comments displayed in chronological order
- Display commenter username
- Display comment time

## Inline Voting

Can vote directly in chat content:

1. See contract recommendation message
2. Click vote button below message
3. Select voting emoji
4. Vote takes effect immediately

## Contract Information

### Display Information

Contract recommendation card displays:

- Contract address
- Chain
- Voting statistics
- Comment list
- Recommender information

### Contract Details

Clicking contract address can:

- View on-chain information (planned)
- View transaction records (planned)
- View holder information (planned)

## Related Documentation

- [Real-time Chat](../user-guide/chat.md)
- [Points System](../features/points-system.md)
