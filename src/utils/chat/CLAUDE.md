# Chat Directory
Utility functions for chat operations including message status creation, participant extraction, and chat retrieval.

## Files

### create-group-message-statuses.ts
Creates message status objects for group chat participants. Sets status to "Sender" for the message author and "Sent" for all other participants.

### extract-friend-ids.ts
Exports two functions to extract friend user IDs from chats by filtering out the current user:
- `extractGroupChatFriendIds`: Returns array of friend IDs from a group chat
- `extractPrivateChatFriendId`: Returns single friend ID from a private chat

### retrieve-group-chats-with-names.ts
Fetches all active group chats for a user from MongoDB and attaches each chat's custom name from the user's preferences.

### retrieve-private-chats-with-names.ts
Fetches all active private chats for a user from MongoDB and attaches each chat's custom name from the user's preferences.
