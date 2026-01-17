# Events Directory
Controllers for Eventfull event CRUD operations and user interactions (registration, invites, pinning).

## Files
### cancel-eventfull-event-registration.ts
Cancels a user's registration for an event. Prevents organizers from canceling and removes user from attendees list.

### create-eventfull-event.ts
Creates a new Eventfull event. Adds event to organizer, co-hosts, and invitees' event lists with appropriate statuses.

### delete-eventfull-event.ts
Soft-deletes an event by setting `isActive` to false.

### invite-friend-to-eventfull-event.ts
Invites a friend to an event. Adds invitee to both the event's invitees list and the friend's eventfullEvents array.

### pin-eventfull-event.ts
Adds an event to user's pinned events list using `$addToSet`.

### remove-pinned-eventfull-event.ts
Removes an event from user's pinned events list.

### respond-to-eventfull-invite.ts
Handles invite responses (Attending, Not Attending, Not Responded). Updates both event and user records accordingly.

### retract-invite-to-eventfull-event.ts
Removes a pending invite. Pulls invitee from event's invitees list and removes event from invitee's eventfullEvents.

### retrieve-events-feed.ts
Returns public, active events with images that are in the future. Uses MongoDB aggregation with event frequency logic (one-time, custom, ongoing).

### sign-up-for-eventfull-event.ts
Registers a user for an event. Handles both direct sign-ups and converting invited users to attendees.

### update-eventfull-event.ts
Updates an event. Adds new invitees; organizers can also add co-hosts.
