# Notifications Directory
Utilities for creating platform-specific push notification messages for AWS SNS.

## create-notifications/

### create-apns-message.ts
Creates iOS push notification payloads for APNS and APNS_SANDBOX with title, body, sound, badge, and custom data fields.

### create-gcm-message.ts
Creates Android push notification payloads for GCM/FCM with title, body, and custom data fields.

### get-platform-application-arn.ts
Returns the appropriate AWS SNS platform application ARN (APNS or FCM) based on device platform.

### return-correct-message-type.ts
Router function that selects and calls the correct message creator (APNS or GCM) based on the target device platform.
