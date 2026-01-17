# Request Validation Directory

Express middleware validators using Joi for request validation. Each file exports a middleware function that validates request data (body, params, or query) against a Joi schema, returning 400 on validation errors or calling `next()` on success. Some validators also fetch and attach database entities to the request object.

## calendar/
Validates calendar-related operations including calendar IDs, event creation (cloud/local), and updates for Google/Microsoft/Local calendars. Uses unified calendar event schemas for consistent validation across providers.
- `validate-calendar-id.ts` - Validates calendarId in params
- `validate-create-cloud-event.ts` - Validates cloud event creation body
- `validate-create-local-calendar-event.ts` - Validates local event creation body
- `validate-update-google-calendar-event.ts` - Validates Google calendar event updates
- `validate-update-local-calendar-event.ts` - Validates local calendar event updates
- `validate-update-microsoft-calendar-event.ts` - Validates Microsoft calendar event updates
- `validate-update-only-show-eventfull-events.ts` - Validates boolean setting toggle

## chat/
Shared chat validators for message pagination, status updates, and text editing.
- `validate-message-pagination-query-params.ts` - Validates pagination query (lastMessageId, limit)
- `validate-updated-message-status.ts` - Validates message status (Read/Delivered)
- `validate-updated-message-text.ts` - Validates updated message text (1-1000 chars)

### group/
Validates group chat operations including chat/message IDs and content.
- `validate-friend-ids.ts` - Validates array of friend IDs (2-6), fetches users
- `validate-group-chat-id-in-params.ts` - Validates groupChatId, fetches group chat
- `validate-group-message-id-in-params.ts` - Validates groupMessageId, fetches message and chat
- `validate-group-message.ts` - Validates new group message content
- `validate-updated-group-chat-name.ts` - Validates chat name updates (1-200 chars)

### private/
Validates private chat operations including chat/message IDs and content.
- `validate-private-chat-id-in-params.ts` - Validates privateChatId, fetches private chat
- `validate-private-message-id-in-params.ts` - Validates privateMessageId, fetches message and chat
- `validate-private-message.ts` - Validates new private message content
- `validate-updated-private-chat-name.ts` - Validates chat name updates (1-200 chars)

## auth/
Validates user authentication operations including login, registration, password changes, and contact verification.
- `validate-add-cloud-user-personal-info.ts` - Validates OAuth user profile completion (firstName, lastName, username)
- `validate-change-password.ts` - Validates password change (contact, currentPassword, newPassword)
- `validate-contact-code.ts` - Validates 6-digit verification code
- `validate-contact.ts` - Validates contact (email/phone) string
- `validate-login.ts` - Validates login credentials with device info
- `validate-register.ts` - Validates full registration with user details
- `validate-user-socket-state.ts` - Validates app state (active/inactive/background)
- `validate-username.ts` - Validates username (min 4 chars)

### google/
Validates Google OAuth callbacks.
- `validate-google-calendar-callback.ts` - Validates Google calendar OAuth code
- `validate-google-login-callback.ts` - Validates Google login OAuth (code, idToken, device info)

### microsoft/
Validates Microsoft OAuth callbacks.
- `validate-microsoft-calendar-callback.ts` - Validates Microsoft calendar OAuth, extracts user from state token
- `validate-microsoft-login-callback.ts` - Validates Microsoft login OAuth code

## admin/

### auth/
Validates admin authentication operations.
- `validate-admin-login.ts` - Validates admin login (contact, password)
- `validate-admin-otp-login.ts` - Validates admin OTP login (email, 6-digit OTP)
- `validate-initial-admin-register-info.ts` - Validates initial admin registration (email, firstName, lastName)
- `validate-secondary-admin-register-info.ts` - Validates secondary registration step (username, password)

### users/
Validates admin user management operations.
- `validate-user-id.ts` - Validates MongoDB ObjectId in params

### events/
Validates admin event management operations.
- `validate-image-urls.ts` - Validates array of image URL objects (imageId, imageURL, isActive)

## search/
Validates search query parameters.
- `validate-search-event-name.ts` - Validates event name search param
- `validate-search-username.ts` - Validates username search param (optional, trimmed)

## social/
Validates social interaction operations (friends, blocking).
- `validate-blocked-user-id.ts` - Validates blockedUserId, fetches user
- `validate-created-at.ts` - Validates createdAt date for friend requests
- `validate-friend-id.ts` - Validates friendId in params, fetches user
- `validate-unblocked-user-id.ts` - Validates unblockedUserId, fetches user

## profile/
Validates user profile settings.
- `validate-color-theme.ts` - Validates color theme (Dark/Light/System Default)

## events/
Validates Eventfull event operations including CRUD for events, types, and categories.
- `validate-create-event-category.ts` - Validates new event category (name, description)
- `validate-create-event-type.ts` - Validates new event type with categories array
- `validate-create-eventfull-event.ts` - Validates new event creation with image count
- `validate-event-category-id.ts` - Validates eventCategoryId in params
- `validate-event-id.ts` - Validates eventId in params
- `validate-event-type-id.ts` - Validates eventTypeId in params
- `validate-eventfull-event-id.ts` - Validates eventfullEventId, fetches event
- `validate-eventfull-invite.ts` - Validates event invite (eventId, friendId), fetches friend
- `validate-response-to-eventfull-event-invite.ts` - Validates invite response (Attending/Not Attending/Not Responded)
- `validate-update-event-category.ts` - Validates event category update with metadata
- `validate-update-event-type.ts` - Validates event type update with metadata
- `validate-update-eventfull-event.ts` - Validates event update with image count
