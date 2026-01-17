# Microsoft Directory
Utilities for Microsoft OAuth authentication, token management, and Outlook calendar integration via Microsoft Graph API.

## Root Files

### msal-config.ts
Configures and exports the MSAL ConfidentialClientApplication instance using environment credentials.

### create-graph-client.ts
Creates an authenticated Microsoft Graph API client from an access token.

### get-key-from-microsoft.ts
JWKS client for fetching Microsoft's public signing keys for JWT verification.

### verify-id-token.ts
Verifies and decodes Microsoft ID tokens using JWKS public keys.

## auth/

### exchange-code-for-token-login-callback.ts
Exchanges OAuth authorization code for login tokens (openid, profile, email scopes).

### save-microsoft-login-tokens.ts
Saves Microsoft login tokens to user record in MongoDB. Creates user if not found.

## calendar/

### convert-unified-to-microsoft.ts
Converts unified calendar event format to Microsoft Graph API Event format.

## calendar/calendar-auth/

### exchange-code-for-token-calendar-callback.ts
Exchanges OAuth authorization code for calendar tokens (Calendars.ReadWrite scope).

### save-microsoft-calendar-tokens.ts
Saves Microsoft calendar access/refresh tokens and expiry to user record.

## calendar/calendar-retrieval/

### convert-microsoft-to-unified.ts
Converts Microsoft Graph API events to unified calendar event format with timezone handling.

### get-microsoft-calendar-tokens.ts
Extracts calendar tokens from user object.

### get-valid-microsoft-calendar-token.ts
Returns valid access token, refreshing if expired.

### refresh-microsoft-calendar-token.ts
Refreshes expired calendar access token using MSAL and updates DB.

### retrieve-and-set-default-calendar-id.ts
Fetches user's default calendar ID from Microsoft Graph and saves to DB.

### save-default-calendar-id-to-db.ts
Persists the default Microsoft calendar ID to user record.

### update-microsoft-calendar-tokens-in-db.ts
Updates calendar tokens in DB after token refresh.
