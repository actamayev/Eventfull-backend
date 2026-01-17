# Events Directory
Utility functions for managing Eventfull events, including creation, invitations, co-host management, and attendance tracking.

## Files

### add-cohosts.ts
Manages co-host additions and removals for events. Validates co-hosts are friends of the organizer, updates both the event's coHosts array and each co-host user's eventfullEvents array.

### add-eventfull-event.ts
Creates a new EventfullEvent document in MongoDB with all event properties (name, price, type, frequency, timing, invitees, co-hosts, etc.). Returns the new event's ObjectId.

### add-invitees.ts
Handles adding and removing invitees from events. Filters invitees to only include friends, prevents duplicates with existing invitees/attendees, and syncs both the event document and user documents.

### cancel-event-registration.ts
Updates a user's attending status to "Not Attending" for an event. Either updates existing entry by index or adds a new entry if not found.

### convert-admin-event-to-eventfull-event.ts
Converts an admin-submitted event into an EventfullEvent model instance with admin-specific defaults (isActive: true, eventReviewable: false, isCreatedByAdmin flag).

### convert-to-eventfull-event.ts
Converts incoming event data into an EventfullEvent model instance for regular users. Filters invitees to only friends and formats invitee/co-host objects with invitation metadata.

### determine-event-status.ts
Returns event temporal status ("Future", "Happening Now", or "Past") based on current time and event frequency type (one-time, custom, or ongoing).

### respond-attending-to-invited-event.ts
Moves a user from the invitees array to the attendees array when they accept an event invitation. Preserves the original invitation metadata.

### update-user-attending-status.ts
Updates a user's attending status to "Attending" for an event. Either updates existing entry by index or adds a new entry if not found.
