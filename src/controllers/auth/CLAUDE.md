# Auth Directory

Express route controllers for authentication, user registration, and third-party OAuth integrations.

## Root files

### add-cloud-user-personal-info.ts
Adds personal information for cloud-authenticated users (Google/Microsoft). Validates username uniqueness before saving.

### add-secondary-contact-method.ts
Allows users to add a secondary email or phone to their account. Validates the contact is not already in use.

### change-password.ts
Handles password changes. Verifies current password, ensures new password differs from old, then updates with hashed password.

### check-if-contact-exists.ts
Real-time endpoint to check if an email or phone number is already registered.

### check-if-username-exists.ts
Real-time endpoint to check if a username is already taken.

### login.ts
Standard login with email/phone and password. Returns JWT, user info, and Google Calendar connection status. Redirects Google/Microsoft users to their respective OAuth flows.

### logout.ts
Clears user's notification token and AWS SNS endpoint ARN on logout.

### register-username.ts
Registers a username for an existing user (used after OAuth signup). Validates uniqueness.

### register.ts
New user registration with email/phone, username, and password. Creates AWS SNS endpoint for push notifications and returns JWT.

### update-user-socket-state.ts
Updates user's app state (foreground/background) in the socket manager for real-time presence.

## google-auth/

### google-calendar-auth-callback.ts
OAuth callback for Google Calendar integration. Exchanges auth code for tokens and saves them to user record.

### google-login-auth-callback.ts
OAuth callback for Google login. Creates/retrieves user, issues JWT, and returns user info with calendar connection status.

### revoke-google-calendar-access.ts
Revokes Google Calendar OAuth tokens and removes synced calendar data from user record.

## microsoft-auth/

### generate-microsoft-calendar-auth-url.ts
Generates Microsoft OAuth URL for calendar integration with Calendars.ReadWrite scope.

### generate-microsoft-login-auth-url.ts
Generates Microsoft OAuth URL for user login with openid/email/profile scopes.

### microsoft-calendar-auth-callback.ts
OAuth callback for Microsoft Calendar integration. Exchanges code for tokens and saves them.

### microsoft-login-auth-callback.ts
OAuth callback for Microsoft login. Verifies ID token, saves tokens, creates/retrieves user, and issues JWT.

### revoke-microsoft-calendar-access.ts
Clears Microsoft Calendar tokens and removes synced calendar data from user record.

## twilio/

### send-email-verification-code.ts
Sends a 6-digit verification code to user's email via SendGrid. Stores code and timestamp in DB.

### send-phone-verification-code.ts
Sends a 6-digit verification code to user's phone via Twilio SMS. Stores code and timestamp in DB.

### verify-user-email-code.ts
Validates email verification code (10-minute expiry). Marks email as verified on success.

### verify-user-phone-code.ts
Validates phone verification code (10-minute expiry). Marks phone as verified on success.
