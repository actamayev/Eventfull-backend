# Classes Directory

Service classes and utilities for AWS integrations and real-time communication.

## Files

### aws-sns-service.ts
Singleton wrapper for AWS SNS. Handles push notification delivery.
- `createPlatformEndpoint` - Register device token with SNS
- `deletePlatformEndpoint` - Remove device from SNS
- `sendNotification` - Send push notification to device

### aws-storage-service.ts
Singleton wrapper for AWS S3. Handles image upload URLs.
- `generatePresignedURL` - Creates 60-second presigned URL for uploading event images

### hash.ts
Static utility for password operations using bcrypt.
- `hashCredentials` - Hash passwords (uses `SALT_ROUNDS` env var, defaults to 10)
- `checkPassword` - Compare plaintext against hash

### notification-helper.ts
Orchestrates notifications via WebSocket (online users) or push (offline/background users).

Handles: friend requests, private messages, group messages, and their status updates.

Pattern: Check if user is online via SocketManager → send via WebSocket if yes, else send push via AwsSnsService.

### socket-manager.ts
Singleton managing Socket.IO connections. Must call `assignIo(io)` before `getInstance()`.

Tracks user connection states: `active` (foreground), `background` (minimized), or disconnected.

Emits events for: friend requests, private/group messages, message status updates.
