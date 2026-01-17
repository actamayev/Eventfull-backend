# Find Directory

Utility functions for finding database entities by ID with optional field selection.

## Files

### find-admin.ts
Finds an admin by ID. Returns Admin or null. Uses `.lean()` for plain objects.

### find-event-category.ts
Finds an event category by ID. Returns EventCategory or null. Uses `.lean()`.

### find-event-type.ts
Finds an event type by ID. Returns EventType or null. Uses `.lean()`.

### find-event.ts
Finds an event by ID. Returns EventfullEvent or null. Does not use `.lean()`.

### find-group-chat.ts
Finds a group chat by ID. Returns GroupChat or null. Uses `.lean()`.

### find-group-message.ts
Finds a group message by ID. Returns GroupMessageWithChatId or null. Uses `.lean()`.

### find-private-chat.ts
Finds a private chat by ID. Returns PrivateChat or null. Uses `.lean()`.

### find-private-message.ts
Finds a private message by ID. Returns PrivateMessageWithChatId or null. Uses `.lean()`.

### find-user.ts
Finds a user by ID. Returns User or null. Does not use `.lean()`.
