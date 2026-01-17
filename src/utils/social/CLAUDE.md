# Social Directory
Utility functions for managing user social relationships (friends and blocks) in MongoDB.

## block/
### block-user.ts
Adds a user to another user's blocked list and updates the blocked user's blockedByUsers list.

### check-if-user-blocked-by-friend.ts
Checks if the current user has been blocked by another user.

### check-if-user-has-blocked-friend.ts
Checks if the current user has blocked another user.

### unblock-user.ts
Removes a user from the blocked list and updates both users' records.

## friend/
### accept-friend-request-helper.ts
Accepts a friend request by adding both users to each other's friends list, clearing the request, and sending a notification.

### are-users-friends.ts
Checks if two users are already friends.

### check-if-incoming-friend-request-exists.ts
Checks if there is a pending incoming friend request from a specific user.

### check-if-outgoing-friend-request-exists.ts
Checks if there is a pending outgoing friend request to a specific user.

### clear-incoming-friend-request.ts
Removes an incoming friend request and the corresponding outgoing request from the sender.

### clear-outgoing-friend-request.ts
Removes an outgoing friend request and the corresponding incoming request from the recipient.

### create-outgoing-friend-request.ts
Creates a new friend request by adding to sender's outgoing and recipient's incoming request lists.

### unfriend-your-friend.ts
Removes two users from each other's friends lists and clears related notifications.
