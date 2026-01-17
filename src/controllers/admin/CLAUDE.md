# Admin Directory

Express controllers for admin panel operations. All controllers follow standard Express request/response patterns with error handling.

## auth/

### add-admin.ts
Registers a new admin by email. Sends verification code via SendGrid and stores initial admin info.

### admin-login-otp.ts
Handles OTP-based login. Verifies email verification code and returns JWT access token.

### admin-login.ts
Standard login with email/username and password. Returns JWT access token on success.

### admin-logout.ts
Simple logout endpoint. Returns success response (JWT invalidation not yet implemented).

### finish-admin-registration.ts
Completes admin registration by setting username and password after OTP verification.

## users/

### retrieve-single-user.ts
Fetches a single user by ID with selected fields (name, email, phone, friends, login history).

### retrieve-users.ts
Lists all users with selected fields. No pagination implemented yet.

## personal-info/

### retrieve-admin-personal-info.ts
Returns authenticated admin's profile info (name, username, email).

## events/

### add-admin-eventfull-event.ts
Creates new event with AWS S3 presigned URLs for image uploads.

### add-image-urls.ts
Updates event with uploaded image URLs after S3 upload completes.

### delete-admin-eventfull-event.ts
Soft-deletes an event by setting isActive to false.

### retrieve-eventfull-events.ts
Lists all active events. No pagination implemented yet.

### retrieve-single-eventfull-event.ts
Fetches single event by ID, filtering to only active images.

### update-admin-eventfull-event.ts
Updates event data and optionally generates new presigned URLs for additional images.

### event-types/

#### add-event-type.ts
Creates new event type or reactivates existing inactive one. Tracks admin who created it.

#### delete-event-type.ts
Soft-deletes event type by setting isActive to false.

#### retrieve-single-event-type.ts
Fetches single event type by ID if active.

#### update-event-type.ts
Updates event type fields.

### event-categories/

#### add-event-category.ts
Creates new event category or reactivates existing inactive one. Tracks admin who created it.

#### delete-event-category.ts
Soft-deletes event category by setting isActive to false.

#### retrieve-single-event-category.ts
Fetches single event category by ID if active.

#### update-event-category.ts
Updates event category and propagates name/description changes to all event types referencing it.
