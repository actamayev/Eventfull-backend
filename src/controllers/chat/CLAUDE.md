# Chat Directory

Express controllers for group and private chat functionality. Each controller handles HTTP requests, interacts with MongoDB models, and sends notifications via NotificationHelper.

## group/chat/

### create-group-chat.ts
Creates a new group chat with multiple participants. Generates personalized chat names for each participant and updates user records.

### edit-group-chat-name.ts
Updates the group chat name for the requesting user only (stored in user's groupChats array).

### retrieve-group-chats.ts
Returns all group chats for the authenticated user with their personalized chat names attached.

### retrieve-single-group-chat.ts
Returns a single group chat by ID with the user's personalized chat name attached.

### retrieve-single-group-message.ts
Returns a single group message from the request context.

## group/message/

### delete-group-message.ts
Soft-deletes a group message (sets isActive: false). Updates lastMessage if needed and notifies participants.

### reply-to-group-message.ts
Creates a new group message as a reply to an existing message. Updates lastMessage and notifies participants.

### retrieve-group-chat-messages.ts
Returns paginated group messages for a chat. Supports cursor-based pagination via lastMessageId and limit params.

### send-group-message.ts
Creates a new group message with message statuses for all participants. Updates lastMessage and notifies participants.

### update-group-message-status.ts
Updates message delivery/read status for the requesting user. Syncs to lastMessage if applicable and notifies participants.

### update-group-message.ts
Edits message text, marks as edited, resets message statuses. Updates lastMessage if applicable and notifies participants.

## private/chat/

### create-private-chat.ts
Creates a new private chat between two users. Sets personalized chat names and updates both users' records.

### edit-private-chat-name.ts
Updates the private chat name for the requesting user only (stored in user's privateChats array).

### retrieve-private-chats.ts
Returns all private chats for the authenticated user with their personalized chat names attached.

### retrieve-single-private-chat.ts
Returns a single private chat by ID with the user's personalized chat name attached.

### retrieve-single-private-message.ts
Returns a single private message from the request context.

## private/message/

### delete-private-message.ts
Soft-deletes a private message (sets isActive: false). Updates lastMessage if needed and notifies the other participant.

### reply-to-private-message.ts
Creates a new private message as a reply to an existing message. Updates lastMessage and notifies the recipient.

### retrieve-private-chat-messages.ts
Returns paginated private messages for a chat. Supports cursor-based pagination via lastMessageId and limit params.

### send-private-message.ts
Creates a new private message. Updates lastMessage and notifies the recipient.

### update-private-message-status.ts
Updates message delivery/read status. Syncs to lastMessage if applicable and notifies the other participant.

### update-private-message.ts
Edits message text, marks as edited, resets status to "Sent". Updates lastMessage if applicable and notifies the other participant.
