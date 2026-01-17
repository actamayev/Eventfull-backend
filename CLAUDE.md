# Eventfull Backend

Express.js + TypeScript backend for the Eventfull mobile app. Handles events, social features, real-time messaging, and calendar integrations.

## Tech Stack

- **Runtime**: Node.js with TypeScript
- **Framework**: Express.js
- **Database**: MongoDB (Mongoose ODM)
- **Real-time**: Socket.IO
- **Auth**: JWT, Google OAuth, Microsoft OAuth
- **Cloud Services**: AWS S3 (images), AWS SNS (push notifications), SendGrid (email), Twilio (SMS)

## Quick Start

```bash
npm install
cp .env.sample .env  # Fill in required values
npm start            # Runs with nodemon + ts-node
```

## Scripts

- `npm start` - Development server with hot reload
- `npm run build` - Compile TypeScript
- `npm run lint` - Run ESLint
- `npm run lint:fix` - Fix ESLint issues
- `npm run type-check` - TypeScript type checking
- `npm run validate` - Lint + type-check

## Environment Variables

See `.env.sample` for required variables:
- `PORT`, `MONGODB_URI`, `JWT_KEY`, `SALT_ROUNDS`
- Google OAuth: `GOOGLE_CLIENT_ID`, `GOOGLE_CLIENT_SECRET`
- Microsoft OAuth: `MICROSOFT_CLIENT_ID`, `MICROSOFT_SECRET_ID`, `MICROSOFT_TENANT_ID`
- AWS: `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `AWS_REGION`, `AWS_FCM_ARN`, `AWS_APNS_ARN`
- SendGrid: `SENDGRID_API_KEY`, `SENDGRID_FROM_EMAIL`

## API Routes

All routes except `/auth`, `/admin/auth`, and `/health` require JWT authentication.

| Base Path | Description |
|-----------|-------------|
| `/admin` | Admin panel (auth, users, events management) |
| `/auth` | User authentication (login, register, OAuth, verification) |
| `/calendar` | Calendar integrations (local, Google, Microsoft) |
| `/chat` | Private and group messaging |
| `/events` | Event CRUD, invites, registration |
| `/lists` | Event types and categories |
| `/profile` | User profile settings |
| `/search` | User and event search |
| `/social` | Friends, blocking |
| `/health` | Health check endpoint |

## Project Structure

```
src/
├── index.ts              # App entry point, Express + Socket.IO setup
├── classes/              # Singleton services (AWS, Socket, Notifications)
├── controllers/          # Route handlers
│   ├── admin/            # Admin endpoints
│   ├── auth/             # Authentication (local, Google, Microsoft, Twilio)
│   ├── calendar/         # Calendar CRUD (local, Google, Microsoft)
│   ├── chat/             # Private and group messaging
│   ├── events/           # Event management
│   ├── lists/            # Static data (event types/categories)
│   ├── profile/          # User profile
│   ├── search/           # Search functionality
│   └── social/           # Friends, blocking
├── middleware/           # Express middleware
│   ├── jwt/              # JWT verification
│   ├── auth/             # Auth guards (contact type, Twilio)
│   ├── calendar/         # Calendar token assignment
│   ├── chat/             # Chat validation (group, private)
│   ├── events/           # Event permission checks
│   ├── joi/              # Joi validation schemas
│   ├── request-validation/ # Request body validators
│   ├── social/           # Friend/block checks
│   └── attach-to-request/ # Request augmentation
├── models/               # Mongoose schemas
│   ├── chat/             # Chat and message models
│   └── *.ts              # User, Event, Admin, etc.
├── routes/               # Express routers
│   ├── admin/            # Admin routes
│   ├── auth/             # Auth routes (Google, Microsoft, Twilio)
│   ├── calendar/         # Calendar routes
│   └── chat/             # Chat routes
├── types/                # TypeScript type definitions
│   ├── admin/            # Admin types
│   └── models/           # Model types
├── utils/                # Helper functions
│   ├── auth-helpers/     # JWT, login, register, AWS, Twilio
│   ├── calendar-misc/    # Calendar event DB operations
│   ├── chat/             # Chat utilities
│   ├── events/           # Event utilities
│   ├── find/             # DB lookup helpers
│   ├── google/           # Google OAuth + Calendar
│   ├── microsoft/        # Microsoft OAuth + Calendar
│   ├── notifications/    # Push notification formatting
│   └── social/           # Friend/block utilities
├── json/                 # Seed data (event types, categories)
└── setup-and-security/   # DB connection
```

## Key Patterns

### Authentication Flow
1. User registers/logs in via local auth or OAuth (Google/Microsoft)
2. Server returns JWT token
3. Client includes token in requests; `jwtVerify` middleware validates
4. Socket.IO connections also authenticated via JWT

### Real-time Messaging
- `SocketManager` singleton manages WebSocket connections
- `NotificationHelper` orchestrates delivery: Socket.IO for online users, AWS SNS push for offline/background
- Message statuses: Sent → Delivered → Read

### Calendar Integration
- Supports Google Calendar and Microsoft Outlook
- Events normalized to `UnifiedCalendarEvent` format
- Local events stored directly in MongoDB

### Event System
- Events have organizers, co-hosts, invitees, and attendees
- Supports one-time, custom, and ongoing event frequencies
- Public events allow open registration; private require invites

## MongoDB Collections

- `users` - User accounts and profiles
- `admins` - Admin accounts
- `eventfull-events` - Events
- `event-types`, `event-categories` - Event categorization
- `private-chats`, `private-messages` - 1:1 messaging
- `group-chats`, `group-messages` - Group messaging
