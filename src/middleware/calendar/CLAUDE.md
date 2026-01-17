# Calendar Middleware

Express middleware for attaching calendar access tokens and IDs to request headers before calendar operations.

## Files

### assign-google-calendar-access-token.ts
Middleware that retrieves a valid Google Calendar access token for the authenticated user and attaches it to `req.headers.googleCalendarAccessToken`. Returns 400 if no token is found.

### assign-microsoft-calendar-id-and-access-token.ts
Middleware that retrieves a valid Microsoft Calendar access token and the user's default calendar ID. Attaches both to request headers (`microsoftCalendarAccessToken`, `microsoftDefaultCalendarId`). If no default calendar ID exists, it retrieves and sets one. Returns 400 if token or calendar ID cannot be obtained.
