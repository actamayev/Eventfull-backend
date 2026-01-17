# Social Directory
Controllers for social features: friend requests, blocking, and relationship management.

## Root files

### accept-friend-request.ts
Accepts an incoming friend request using the createdAt timestamp for identification.

### block-another-user.ts
Blocks a user. Also unfriends them if friends, clears any pending friend requests, and retracts notifications.

### decline-friend-request.ts
Declines an incoming friend request by clearing it from the user's incoming requests.

### retract-friend-request.ts
Cancels a previously sent outgoing friend request and retracts the associated notification.

### send-friend-request.ts
Sends a friend request to another user. Validates no existing outgoing or incoming request exists first.

### unblock-another-user.ts
Unblocks a previously blocked user after verifying they are currently blocked.

### unfriend-another-user.ts
Removes an existing friend from the user's friends list.

## list/

### list-blocked-users.ts
Returns the authenticated user's list of blocked users.

### list-friends.ts
Returns the authenticated user's friends list.

### list-incoming-friend-requests.ts
Returns pending friend requests received by the authenticated user.

### list-outgoing-friend-requests.ts
Returns pending friend requests sent by the authenticated user.
