# Social Directory
Express middleware for validating social interactions (friend requests, blocking/unblocking users).

## block/
### check-if-blocked-user-blocked-user.ts
Prevents blocking a user who has already blocked you. Returns 400 if the target user has blocked the requesting user.

### check-if-user-blocked-blocked-user.ts
Prevents duplicate blocks. Returns 400 if the requesting user has already blocked the target user.

## friend/
### confirm-friend-hasnt-blocked-user.ts
Blocks friend actions if the target friend has blocked the requesting user. Returns 400 with block notification.

### confirm-incoming-friend-request-exists.ts
Validates that a pending incoming friend request exists before accepting. Returns 400 if no request found.

### confirm-user-hasnt-blocked-friend.ts
Prevents friend actions with users you have blocked. Returns 400 if the target is on your block list.

### confirm-user-not-friending-self.ts
Prevents users from sending friend requests to themselves. Returns 400 on self-friending attempt.

### confirm-users-are-friends.ts
Validates that two users are already friends. Returns 400 if not friends (used for friend-required actions).

### confirm-users-are-not-friends.ts
Validates that two users are not already friends. Returns 400 if already friends (used when sending new requests).

## unblock/
### check-if-unblocked-user-blocked-user.ts
Checks if the user being unblocked has blocked you. Returns 400 if they have blocked you.
