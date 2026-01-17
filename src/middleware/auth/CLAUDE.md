# Auth Directory
Express middleware for authentication guards and contact type determination.

## Root files

### confirm-user-has-google-calendar.ts
Validates that the authenticated user has a Google Calendar access token. Returns 400 if missing.

### confirm-user-has-microsoft-calendar.ts
Validates that the authenticated user has a Microsoft Calendar access token. Returns 400 if missing.

## determine-contact-type/

### determine-contact-type.ts
Determines if `req.body.contact` is an email or phone number using the `emailOrPhone` utility. Sets `req.contactType`.

### determine-change-password-contact-type.ts
Same as above but reads from `req.body.changePasswordObject.contact`. Sets `req.contactType`.

### determine-register-contact-type.ts
Same as above but reads from `req.body.registerInformationObject.contact`. Sets `req.body.registerInformationObject.contactType`.

## twilio/

### confirm-user-has-email.ts
Validates user has an email address registered. Returns 400 if undefined.

### confirm-user-has-phone-number.ts
Validates user has a phone number registered. Returns 400 if undefined.

### confirm-user-has-email-verification-code.ts
Validates user has a pending email verification code. Returns 400 if undefined.

### confirm-user-has-phone-verification-code.ts
Validates user has a pending phone verification code. Returns 400 if undefined.

### confirm-user-email-not-verified.ts
Ensures user's email is NOT yet verified (for sending new verification codes). Returns 400 if already verified.

### confirm-user-phone-not-verified.ts
Ensures user's phone is NOT yet verified (for sending new verification codes). Returns 400 if already verified.
