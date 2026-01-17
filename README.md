# Eventfull Backend

A Node.js/Express backend API for the Eventfull mobile application - a social events platform that helps users discover, create, and manage events while connecting with friends.

## Features

- **Event Management**: Create, update, and discover events with support for one-time, recurring, and ongoing schedules
- **Social Networking**: Friend requests, blocking, and social connections
- **Real-time Messaging**: Private 1:1 and group chat with read receipts via Socket.IO
- **Calendar Integration**: Sync with Google Calendar and Microsoft Outlook
- **Push Notifications**: AWS SNS integration for iOS (APNS) and Android (FCM)
- **Multi-auth Support**: Local authentication, Google OAuth, and Microsoft OAuth
- **Admin Dashboard API**: Separate admin endpoints for platform management

## Tech Stack

| Category | Technology |
|----------|------------|
| Runtime | Node.js |
| Language | TypeScript |
| Framework | Express.js |
| Database | MongoDB with Mongoose ODM |
| Real-time | Socket.IO |
| Authentication | JWT, Google OAuth 2.0, Microsoft MSAL |
| Cloud Storage | AWS S3 (event images) |
| Push Notifications | AWS SNS |
| Email | SendGrid |
| SMS | Twilio |
| Validation | Joi |

## Prerequisites

- Node.js (v18+ recommended)
- MongoDB instance (local or Atlas)
- AWS account (for S3 and SNS)
- Google Cloud Console project (for OAuth and Calendar API)
- Microsoft Azure AD app registration (for OAuth and Calendar API)
- SendGrid account
- Twilio account (optional, for SMS verification)

## Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd Eventfull-backend
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Configure environment variables**
   ```bash
   cp .env.sample .env
   ```

   Edit `.env` and fill in all required values (see [Environment Variables](#environment-variables)).

4. **Start the development server**
   ```bash
   npm start
   ```

   The server will start on the configured PORT (default: 8000).

## Scripts

| Command | Description |
|---------|-------------|
| `npm start` | Start development server with hot reload (nodemon + ts-node) |
| `npm run build` | Compile TypeScript to JavaScript |
| `npm run lint` | Run ESLint on all TypeScript files |
| `npm run lint:fix` | Run ESLint and auto-fix issues |
| `npm run type-check` | Run TypeScript compiler without emitting |
| `npm run validate` | Run both lint and type-check |

## Environment Variables

Create a `.env` file based on `.env.sample`:

```env
# Server
PORT=8000

# Security
SALT_ROUNDS=10
JWT_KEY=your-secret-jwt-key

# Database
MONGODB_URI=mongodb://localhost:27017/eventfull

# Google OAuth & Calendar
GOOGLE_CLIENT_ID=your-google-client-id
GOOGLE_CLIENT_SECRET=your-google-client-secret

# Microsoft OAuth & Calendar
MICROSOFT_CLIENT_ID=your-microsoft-client-id
MICROSOFT_SECRET_ID=your-microsoft-secret
MICROSOFT_TENANT_ID=your-microsoft-tenant-id

# SendGrid (Email)
SENDGRID_API_KEY=your-sendgrid-api-key
SENDGRID_FROM_EMAIL=noreply@yourdomain.com

# AWS
AWS_ACCESS_KEY_ID=your-aws-access-key
AWS_SECRET_ACCESS_KEY=your-aws-secret-key
AWS_REGION=us-east-1

# AWS SNS (Push Notifications)
AWS_FCM_ARN=arn:aws:sns:region:account:app/GCM/app-name
AWS_APNS_ARN=arn:aws:sns:region:account:app/APNS/app-name
```

## API Documentation

### Base URL
```
http://localhost:8000
```

### Authentication

Most endpoints require a valid JWT token in the Authorization header:
```
Authorization: Bearer <token>
```

### Endpoints Overview

#### Authentication (`/auth`)
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/auth/register` | Register new user |
| POST | `/auth/login` | Login with email/phone and password |
| POST | `/auth/logout` | Logout (requires auth) |
| POST | `/auth/change-password` | Change password (requires auth) |
| POST | `/auth/google-auth/login-callback` | Google OAuth callback |
| POST | `/auth/microsoft-auth/login-callback` | Microsoft OAuth callback |
| POST | `/auth/twilio-auth/send-phone-verification-code` | Send SMS code |
| POST | `/auth/twilio-auth/verify-user-phone-code` | Verify SMS code |

#### Events (`/events`) - Requires Auth
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/events/retrieve-events` | Get events feed |
| GET | `/events/get-event/:eventId` | Get single event |
| POST | `/events/create-eventfull-event` | Create new event |
| POST | `/events/update-eventfull-event` | Update event |
| POST | `/events/delete-eventfull-event/:eventfullEventId` | Delete event |
| POST | `/events/invite-friend-to-eventfull-event` | Invite friend |
| POST | `/events/respond-to-eventfull-invite` | Accept/decline invite |
| POST | `/events/sign-up-for-eventfull-event/:eventfullEventId` | Join public event |
| POST | `/events/pin-eventfull-event/:eventfullEventId` | Pin event |

#### Social (`/social`) - Requires Auth
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/social/get-friends` | List friends |
| GET | `/social/get-incoming-friend-requests` | List incoming requests |
| GET | `/social/get-outgoing-friend-requests` | List outgoing requests |
| POST | `/social/send-friend-request/:friendId` | Send friend request |
| POST | `/social/accept-friend-request/:friendId` | Accept request |
| POST | `/social/decline-friend-request/:friendId` | Decline request |
| POST | `/social/unfriend-another-user/:friendId` | Remove friend |
| POST | `/social/block-another-user` | Block user |
| POST | `/social/unblock-another-user` | Unblock user |

#### Chat (`/chat`) - Requires Auth
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/chat/private/retrieve-chats-list` | List private chats |
| POST | `/chat/private/create-chat/:friendId` | Start private chat |
| POST | `/chat/private/send-message/:privateChatId` | Send message |
| GET | `/chat/group/retrieve-chats-list` | List group chats |
| POST | `/chat/group/create-chat` | Create group chat |
| POST | `/chat/group/send-message/:groupChatId` | Send group message |

#### Calendar (`/calendar`) - Requires Auth
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/calendar/local-calendar/get-all-calendar-events` | Get local events |
| POST | `/calendar/local-calendar/create-calendar-event` | Create local event |
| GET | `/calendar/google-calendar/get-calendar-events` | Get Google events |
| GET | `/calendar/microsoft-calendar/get-calendar-events` | Get Microsoft events |

#### Search (`/search`) - Requires Auth
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/search/username/:username` | Search users |
| GET | `/search/event-name/:eventName` | Search events |

#### Admin (`/admin`)
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/admin/auth/login` | Admin login |
| POST | `/admin/auth/add-admin` | Register admin |
| GET | `/admin/users/get-users` | List all users |
| GET | `/admin/events/get-events` | List all events |

#### Health Check
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/health` | Server health check |

### WebSocket Events

Connect to Socket.IO at the server root with JWT authentication:

```javascript
const socket = io('http://localhost:8000', {
  auth: { token: 'your-jwt-token' }
});
```

#### Events Emitted by Server
| Event | Description |
|-------|-------------|
| `connected` | Connection established |
| `friend-request` | New friend request received |
| `accept-friend-request` | Friend request accepted |
| `private-message` | New private message |
| `group-message` | New group message |
| `update-private-message-status` | Message read/delivered |
| `update-group-message-status` | Group message status update |

## Project Structure

```
├── src/
│   ├── index.ts                 # Application entry point
│   ├── classes/                 # Singleton services
│   │   ├── aws-sns-service.ts   # Push notification service
│   │   ├── aws-storage-service.ts # S3 presigned URLs
│   │   ├── hash.ts              # Password hashing
│   │   ├── notification-helper.ts # Notification orchestration
│   │   └── socket-manager.ts    # WebSocket management
│   ├── controllers/             # Request handlers
│   ├── middleware/              # Express middleware
│   │   ├── jwt/                 # JWT verification
│   │   ├── request-validation/  # Joi validators
│   │   └── ...                  # Domain-specific middleware
│   ├── models/                  # Mongoose schemas
│   ├── routes/                  # Express routers
│   ├── types/                   # TypeScript definitions
│   ├── utils/                   # Helper functions
│   ├── json/                    # Seed data
│   └── setup-and-security/      # DB connection
├── .env.sample                  # Environment template
├── .eslintrc.json              # ESLint configuration
├── tsconfig.json               # TypeScript configuration
├── package.json                # Dependencies and scripts
└── README.md                   # This file
```

## Database Schema

### Collections

- **users** - User accounts, profiles, social connections, calendar data
- **admins** - Admin accounts for platform management
- **eventfull-events** - Events with organizers, attendees, schedules
- **event-types** - Event type definitions (Concert, Workshop, etc.)
- **event-categories** - Event categories (Entertainment, Sports, etc.)
- **private-chats** - 1:1 chat metadata with last message
- **private-messages** - Individual private messages
- **group-chats** - Group chat metadata (3+ participants)
- **group-messages** - Individual group messages

## Development

### Code Style

The project uses ESLint with TypeScript rules. Run linting before committing:

```bash
npm run validate
```

### Adding New Features

1. Define types in `src/types/`
2. Create Mongoose model in `src/models/`
3. Add validation middleware in `src/middleware/request-validation/`
4. Implement controller in `src/controllers/`
5. Define routes in `src/routes/`
6. Add any utility functions in `src/utils/`

### Middleware Pattern

Routes follow a consistent middleware chain:
```
validation → authentication → authorization → business logic checks → controller
```

Example:
```typescript
router.post(
  "/send-message/:privateChatId",
  validatePrivateMessage,        // Validate request body
  validatePrivateChatIdInParams, // Validate params
  extractFriendFromChat,         // Extract data
  confirmUserIsPrivateChatParticipant, // Authorization
  confirmUserHasntBlockedFriend, // Business logic
  sendPrivateMessage             // Controller
)
```

## Deployment

### Build for Production

```bash
npm run build
```

This compiles TypeScript to JavaScript in the `dist/` directory.

### Production Start

```bash
node dist/index.js
```

### Environment Considerations

- Set `NODE_ENV=production`
- Use a process manager like PM2
- Configure proper CORS origins
- Enable HTTPS via reverse proxy (nginx, etc.)
- Set up MongoDB replica set for production

## License

ISC
