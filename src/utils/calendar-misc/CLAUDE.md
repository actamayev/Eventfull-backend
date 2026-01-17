# Calendar Misc Directory
Utility functions for managing calendar events in the MongoDB user document's `calendarData` array.

## Files

### add-cloud-event-to-db.ts
Adds a new cloud calendar event (Google, etc.) to a user's `calendarData` array. Sets the source, marks as active, and defaults timezone to America/New_York.

### delete-db-calendar-event.ts
Deletes a calendar event by ID. Supports soft delete (sets `isActive: false`) or hard delete (removes from array).

### save-incoming-unified-calendar-events.ts
Syncs incoming events from a cloud source with the database. Removes events no longer in the source, adds new events, and updates changed events. Uses field-level comparison to detect changes.

### update-unified-event-in-db.ts
Updates an existing calendar event in the user's `calendarData` array by finding its index and replacing the entire event object.
