# Types Directory

Global TypeScript type declarations for the Eventfull backend.

## Root Files

### auth.d.ts
Authentication-related types: login/register objects, password change, Google OAuth, user field definitions for local vs cloud auth.

### chat.d.ts
Chat display types: `GroupChatWithName`, `PrivateChatWithName`, `LastMessage*` types for retrieving chats, `MessageStatuses` ("Sent" | "Delivered" | "Read" | "Sender").

### custom-express.d.ts
Express Request augmentation. Adds `user`, `admin`, `privateChat`, `groupChat`, `friend`, `event`, etc. to `Express.Request`.

### dayjs-plugin-utc.d.ts
Module declaration for dayjs UTC plugin.

### environment.d.ts
`ProcessEnv` types for all environment variables: MongoDB, JWT, AWS (S3/SNS), Google/Microsoft OAuth, SendGrid.

### frontend.d.ts
`FrontEndScreens` type for navigation targets: "Events Feed", "Search", "Chat", "Calendar", "Profile", chat screens.

### search.d.ts
`UserWithFriendStatus` interface for search results.

### social.d.ts
Core social types: `SocialData` (userId + username), `SocialDataWithTimestamp`, `AdminSocialData`.

### socket.io.d.ts
Socket.IO augmentation: adds `userId` to `Socket` interface.

### unified-calendar.d.ts
`UnifiedCalendarEvent` type that normalizes Google and Microsoft calendar events into a common format.

### utils.d.ts
Common utility types:
- `IDInterface`, `TimestampsInterface` - Mongoose document base types
- `JwtPayload`, `AdminJwtPayload` - JWT token payloads
- `EmailOrPhone`, `AuthSources`, `DevicePlatforms`, `AppStates`
- `AttendingStatuses`, `UserConnectionInfo`, `NotificationData`

## admin/

### admin-auth.d.ts
Admin authentication types: `AdminLoginInformation`, `AdminLoginOTPInformation`, `InitialAdminRegisterInformation`, `SecondaryAdminRegisterInformation`.

## models/

Mongoose model type definitions.

### admin.d.ts
`Admin` interface: firstName, lastName, email, username, password, loginHistory, email verification fields.

### chat.d.ts
Chat and message model types:
- `Chat`, `PrivateChat`, `GroupChat` - chat structures
- `Message`, `PrivateMessage`, `GroupMessage` - message structures
- `*WithChatId` variants - messages with their parent chat reference

### events.d.ts
Event-related types:
- `EventFrequency`: "one-time" | "custom" | "ongoing"
- `EventCategory`, `EventType` - categorization
- `EventfullEvent` - main event model with invitees, coHosts, attendees
- `EventfullCalendarEvent` - event in user's calendar
- Time structures: `BaseEventTime`, `OngoingEvents`, `EventDuration`

### user.d.ts
`User` interface - comprehensive user model including:
- Auth: authMethod, tokens (Google/Microsoft), verification codes
- Social: friends, friend requests, blocked users
- Chat: privateChats, groupChats
- Calendar: calendarData, eventfullEvents, eventPins
- Settings: colorTheme, notification endpoints
