# Google Directory
Utilities for Google OAuth authentication and Google Calendar integration.

## Root Files
### create-google-auth-client.ts
Creates an OAuth2Client instance using Google client credentials from environment variables.

## auth/
### extract-google-user-from-tokens.ts
Verifies Google ID token, exchanges auth code for tokens, and saves login credentials. Returns user payload and token response.

### save-google-login-tokens.ts
Saves Google login tokens to the database. Creates new user if needed or updates existing Google user's tokens.

## calendar/
### convert-unified-to-google.ts
Converts UnifiedCalendarEvent to Google Calendar event format. Handles all-day events, recurrence rules, and attendees.

### create-google-calendar-client.ts
Creates an authenticated Google Calendar API client using an access token.

### does-user-have-google-calendar.ts
Checks if a user has connected their Google Calendar by verifying access token existence.

## calendar/calendar-auth/
### save-google-calendar-tokens.ts
Saves Google Calendar OAuth tokens (access, refresh, expiry) to the user's database record.

## calendar/calendar-retrieval/
### convert-google-to-unified.ts
Converts Google Calendar events to UnifiedCalendarEvent format. Handles date/time parsing, recurrence patterns, and attendee mapping.

### get-google-calendar-tokens.ts
Extracts Google Calendar tokens from a user object.

### get-valid-google-calendar-token.ts
Returns a valid access token, refreshing it if expired or missing.

### refresh-google-calendar-token.ts
Refreshes an expired Google Calendar access token using the refresh token and updates the database.

### update-google-calendar-tokens-in-db.ts
Updates Google Calendar tokens in the database after a token refresh.
