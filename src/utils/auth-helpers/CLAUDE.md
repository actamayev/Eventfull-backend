# Auth Helpers Directory

Utility functions for authentication, authorization, JWT management, and user/admin registration flows.

## Root Files

### add-login-record.ts
Appends a login timestamp to user or admin loginHistory array in MongoDB.

### add-non-local-auth-user-to-db.ts
Creates a new user record for OAuth/cloud auth (Google, Apple, etc.) with AWS SNS endpoint for push notifications.

### add-secondary-contact-method-to-db.ts
Adds a secondary email or phone to an existing user, marking it as unverified.

### does-admin-email-exist.ts
Case-insensitive check if an admin email already exists in the database.

### does-contact-exist.ts
Case-insensitive check if an email or phone number is already registered to a user.

### does-username-exist.ts
Case-insensitive check if a username exists for either users or admins.

### get-decoded-admin-id.ts
Extracts and verifies adminId from a JWT access token.

### get-decoded-id.ts
Extracts and verifies userId from a JWT access token.

### is-same-contact-method.ts
Checks if the provided contact matches the user's existing email or phone.

## jwt/

### create-and-sign-admin-jwt.ts
Creates a JWT token containing the admin ID payload.

### create-and-sign-jwt.ts
Creates a JWT token containing the user ID and isNewUser flag.

### sign-jwt.ts
Core JWT signing function using the JWT_KEY environment variable.

## login/

### determine-admin-login-type.ts
Detects if admin login input is an email or username.

### determine-login-type.ts
Detects if user login input is an email, US phone number, or username.

### retrieve-admin-from-contact.ts
Fetches admin record by email or username (case-insensitive).

### retrieve-user-from-contact.ts
Fetches user record by email, phone, or username (case-insensitive).

## register/

### admin-register-helpers.ts
- `addInitialAdminInfo`: Creates admin with name and email
- `addUsernameAndPassword`: Updates admin with credentials

### register-helpers.ts
- `hashPassword`: Hashes password using Hash class
- `addLocalUser`: Creates local auth user with hashed password and AWS SNS endpoint
- `addCloudUserPersonalData`: Updates OAuth user with personal details

## aws/

### get-user-arn.ts
Returns the appropriate AWS SNS endpoint ARN based on user's device platform (iOS/Android).

### update-arn.ts
Creates a new AWS SNS platform endpoint and updates user's ARN and notification token.

## twilio/

### generate-verification-code.ts
Generates a random 6-digit numeric verification code for SMS/email verification.
