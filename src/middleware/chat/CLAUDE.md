# Chat Directory
Express middleware for validating chat operations (group and private chats).

## group/
### confirm-friends-have-not-blocked-eachother.ts
Validates that no pair of friends in the chat have blocked each other.

### confirm-group-chat-doesnt-exist.ts
Ensures a group chat with the exact same participants doesn't already exist.

### confirm-group-message-sent-by-other-user.ts
Prevents users from marking their own messages as read/delivered.

### confirm-group-message-sent-by-user.ts
Verifies the current user is the sender of a group message.

### confirm-group-message-status-is-new.ts
Validates that the message status update is different from the current status.

### confirm-user-hasnt-blocked-any-friend.ts
Checks that the current user hasn't blocked any of the specified friends.

### confirm-user-is-friends-with-each-participant.ts
Verifies the current user is friends with all specified participants.

### confirm-user-is-group-chat-participant.ts
Confirms the current user is a participant in the group chat.

### extract-friends-from-chat.ts
Extracts and attaches friend User objects from a group chat to `req.friends`.

## private/
### confirm-private-chat-doesnt-exist.ts
Ensures a private chat between the user and friend doesn't already exist.

### confirm-private-message-sent-by-other-user.ts
Prevents users from marking their own messages as read/delivered.

### confirm-private-message-sent-by-user.ts
Verifies the current user is the sender of a private message.

### confirm-private-message-status-is-new.ts
Validates that the message status update is different from the current status.

### confirm-user-is-private-chat-participant.ts
Confirms the current user is a participant in the private chat.

### extract-friend-from-chat.ts
Extracts and attaches the friend User object from a private chat to `req.friend`.
