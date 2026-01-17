# Events Directory

Express middleware functions for validating event-related operations. Each middleware checks specific conditions and either calls `next()` to continue or returns an error response.

## Files

### check-if-event-capacity-full.ts
Checks if event has reached its capacity limit. Blocks attendance if `attendees.length >= eventCapacity`.

### check-if-user-attending-eventfull-event.ts
Sets `req.isUserAttendingEvent` boolean by checking if user is in attendees list or is the organizer.

### confirm-able-to-invite-friend.ts
Validates friend can be invited: not already attending, hasn't declined, and not already invited.

### confirm-event-frequency-attributes.ts
Validates required time attributes based on event frequency type (one-time, custom, or ongoing).

### confirm-event-is-actve.ts
Blocks operations on deleted events by checking `event.isActive` flag.

### confirm-event-is-inviteable.ts
Checks if event allows invited users to invite others via `canInvitedUsersInviteOthers` flag.

### confirm-event-is-not-pinned.ts
Ensures event is not already in user's pins before allowing pin action.

### confirm-event-is-pinned.ts
Ensures event is pinned before allowing unpin action.

### confirm-event-is-public.ts
Blocks operations that require public events by checking `eventPublic` flag.

### confirm-event-organizer-not-blocking-friend.ts
Prevents inviting a friend who is blocked by the event organizer.

### confirm-event-organizer-not-blocking-user.ts
Prevents user from attending if blocked by event organizer.

### confirm-invited-user-has-not-responded.ts
Ensures invited user hasn't already responded (attending or declined) before allowing certain operations.

### confirm-inviter-is-already-invited-or-host.ts
Ensures user is invited, a co-host, or organizer before allowing them to invite others.

### confirm-not-inviting-themselves.ts
Prevents users from inviting themselves to events.

### confirm-user-is-event-organizer-or-cohost.ts
Authorizes event modifications only for organizers or co-hosts. Sets `req.organizerOrCoHost` to indicate role.

### confirm-user-not-blocking-event-organizer.ts
Prevents user from attending events where they have blocked the organizer.
