# Routes Directory

Express router definitions. All routes use middleware chains for validation and authorization.

## Root Files

### events-routes.ts
Event management for users. Base path: `/events`
- POST `/create-eventfull-event` - Create new event
- POST `/respond-to-eventfull-invite` - Accept/decline invite
- POST `/invite-friend-to-eventfull-event` - Invite friend
- POST `/retract-invite-to-eventfull-event` - Cancel invite
- POST `/update-eventfull-event` - Update event (organizer/cohost only)
- POST `/delete-eventfull-event/:eventfullEventId` - Delete event
- POST `/pin-eventfull-event/:eventfullEventId` - Pin event
- POST `/remove-pinned-eventfull-event/:eventfullEventId` - Unpin event
- POST `/sign-up-for-eventfull-event/:eventfullEventId` - Join public event
- POST `/cancel-eventfull-event-registration/:eventfullEventId` - Leave event
- GET `/retrieve-events` - Get events feed
- GET `/get-event/:eventId` - Get single event

### lists-routes.ts
Static data lists. Base path: `/lists`
- GET `/get-event-types` - All event types
- GET `/get-event-categories` - All event categories

### profile-routes.ts
User profile settings. Base path: `/profile`
- POST `/change-color-theme` - Update theme preference

### search-routes.ts
Search functionality. Base path: `/search`
- GET `/username/:username` - Search users by username
- GET `/event-name/:eventName` - Search events by name

### social-routes.ts
Friend and block management. Base path: `/social`
- POST `/send-friend-request/:friendId`
- POST `/accept-friend-request/:friendId`
- POST `/decline-friend-request/:friendId`
- POST `/retract-friend-request/:friendId`
- POST `/unfriend-another-user/:friendId`
- POST `/block-another-user`
- POST `/unblock-another-user`
- GET `/get-incoming-friend-requests`
- GET `/get-outgoing-friend-requests`
- GET `/get-blocked-users`
- GET `/get-friends`

## admin/

Admin panel routes. All routes except `/auth` require `adminJwtVerify`.

### admin-routes.ts
Router aggregator mounting subroutes:
- `/auth` → auth-routes
- `/personal-info` → personal-info-routes (protected)
- `/events` → events-routes (protected)
- `/users` → users-routes (protected)

### auth-routes.ts
Admin authentication. Base path: `/admin/auth`
- POST `/login` - Admin login
- POST `/add-admin` - Register new admin (initial step)
- POST `/otp-login` - OTP-based login
- POST `/finish-admin-registration` - Complete registration (protected)
- POST `/logout`

### events-routes.ts
Admin event management. Base path: `/admin/events`
- CRUD for events, event types, and event categories
- POST `/add-image-urls/:eventfullEventId` - Add S3 image URLs

### personal-info-routes.ts
Base path: `/admin/personal-info`
- GET `/retrieve-personal-data` - Get admin profile

### users-routes.ts
Base path: `/admin/users`
- GET `/get-users` - List all users
- GET `/get-user/:userId` - Get single user

## auth/

User authentication routes.

### auth-routes.ts
Main auth router. Base path: `/auth`
- POST `/login`, `/register`, `/logout`
- POST `/change-password` (protected)
- POST `/register-username` (protected)
- POST `/does-username-exist`, `/does-contact-exist`
- POST `/add-cloud-user-personal-info` (protected)
- POST `/add-secondary-contact` (protected)
- POST `/update-user-socket-state` (protected)
- Mounts: `/google-auth`, `/microsoft-auth`, `/twilio-auth`

### google-auth-routes.ts
Base path: `/auth/google-auth`
- POST `/login-callback` - Handle Google OAuth callback
- POST `/calendar-callback` - Link Google Calendar (protected)
- POST `/revoke-google-calendar-access` - Unlink calendar (protected)

### microsoft-auth-routes.ts
Base path: `/auth/microsoft-auth`
- GET `/generate-login-auth-url`, `/generate-calendar-auth-url`
- POST `/login-callback`
- GET `/calendar-callback`
- POST `/revoke-microsoft-calendar-access` (protected)

### twilio-auth-routes.ts
Phone/email verification. Base path: `/auth/twilio-auth` (all protected)
- POST `/send-phone-verification-code`, `/verify-user-phone-code`
- POST `/send-email-verification-code`, `/verify-user-email-code`

## calendar/

Calendar integration routes.

### calendar-routes.ts
Router aggregator mounting:
- `/local-calendar`, `/google-calendar`, `/microsoft-calendar`

### local-calendar-routes.ts
Local calendar events stored in DB. Base path: `/calendar/local-calendar`
- POST `/create-calendar-event`
- GET `/get-all-calendar-events`
- POST `/update-calendar-event`
- DELETE `/delete-calendar-event/:calendarId`
- GET `/get-pinned-events`
- POST `/update-only-show-eventfull-events`
- GET `/get-only-show-eventfull-events`

### google-calendar-routes.ts
Google Calendar sync. Base path: `/calendar/google-calendar`
- CRUD operations with `assignGoogleCalendarAccessToken` middleware

### microsoft-calendar-routes.ts
Microsoft Calendar sync. Base path: `/calendar/microsoft-calendar`
- CRUD operations with `assignMicrosoftCalendarIdAndAccessToken` middleware

## chat/

Messaging routes.

### chat-routes.ts
Router aggregator mounting:
- `/private` → private-messages-routes
- `/group` → group-messages-routes

### private-messages-routes.ts
1:1 messaging. Base path: `/chat/private`
- POST `/create-chat/:friendId`
- POST `/send-message/:privateChatId`
- GET `/retrieve-chats-list`
- GET `/retrieve-single-chat/:privateChatId`
- GET `/retrieve-single-message/:privateMessageId`
- POST `/update-message-status/:privateMessageId` - Mark delivered/read
- POST `/update-message/:privateMessageId` - Edit message
- DELETE `/delete-message/:privateMessageId`
- POST `/edit-chat-name/:privateChatId`
- GET `/retrieve-messages-from-chat/:privateChatId` - Paginated
- POST `/reply-to-message/:privateMessageId`

### group-messages-routes.ts
Group messaging. Base path: `/chat/group`
- Same structure as private messages but for groups (3+ participants)
- POST `/create-chat` - Requires array of friendIds
