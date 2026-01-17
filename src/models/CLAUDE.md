# Models Directory

Mongoose schemas and models for MongoDB collections.

## Root Files

### admin-model.ts
`AdminModel` - Admin users. Collection: `admins`
- Fields: firstName, lastName, email (unique), username (unique sparse), password, loginHistory, email verification

### calendar-data-model.ts
`calendarDataSchema` - Embedded schema (not a model) for unified calendar events from Google/Microsoft.
- Exports `unifiedDateTimeSchema` for reuse

### event-category-model.ts
`EventCategoryModel` - Event categories. Collection: `event-categories`
- Fields: eventCategoryName (unique), description, isActive, createdBy (admin)

### event-type-model.ts
`EventTypeModel` - Event types containing categories. Collection: `event-types`
- Fields: eventTypeName (unique), description, categories[], isActive, createdBy (admin)
- Exports `eventCategoriesSchema` for embedding

### eventfull-event-model.ts
`EventfullEventModel` - Main events. Collection: `eventfull-events`
- Fields: eventName, eventPrice, eventType (ref), eventFrequency, address, eventDescription
- Participants: invitees[], attendees[], coHosts[], organizer
- Timing: singularEventTime, customEventDates[], ongoingEventTimes[]
- Other: eventCapacity, eventImages[], eventURL, createdBy

### user-model.ts
`UserModel` - App users. Collection: `users`
- Auth: authMethod, password, Google/Microsoft tokens
- Profile: firstName, lastName, username (unique), email (unique sparse), phoneNumber (unique sparse)
- Social: friends[], incomingFriendRequests[], outgoingFriendRequests[], blockedUsers[]
- Chat: privateChats[], groupChats[]
- Calendar: calendarData[], eventfullEvents[], eventPins[]
- Settings: colorTheme, notification endpoints (ios/android ARN)
- Verification: email/phone verification codes and timestamps

## chat/

Shared schemas for chat functionality.

### message-status-model.ts
`messageStatusSchema` - Embedded schema for group message read receipts (userId, username, messageStatus).

### social-data-model.ts
Reusable embedded schemas:
- `socialDataSchema` - userId + username
- `socialDataWithTimestampSchema` - adds createdAt
- `adminData` - adminId + username

## chat/group/

### group-chat-model.ts
`GroupChatModel` - Group conversations. Collection: `group-chats`
- Requires 3+ participants
- Fields: participantDetails[], lastMessage, isActive

### group-message-model.ts
`GroupMessageModel` - Group messages. Collection: `group-messages`
- Fields: groupChatId (ref), senderDetails, text, messageStatuses[], isTextEdited, replyTo, isActive

## chat/private/

### private-chat-model.ts
`PrivateChatModel` - 1:1 conversations. Collection: `private-chats`
- Limited to 2 participants
- Fields: participantDetails[], lastMessage, isActive

### private-message-model.ts
`PrivateMessageModel` - Private messages. Collection: `private-messages`
- Fields: privateChatId (ref), senderDetails, text, messageStatus, isTextEdited, replyTo, isActive
