# Calendar Directory

Express controllers for calendar event management. Supports Google Calendar, Microsoft Calendar, and local (app-only) events using a unified event format.

## Root files

### get-all-db-calendar-events.ts
Returns all active calendar events stored in the user's database record.

### get-only-show-eventfull-events.ts
Retrieves the user's `onlyShowEventfullEvents` preference setting.

### update-only-show-eventfull-events.ts
Updates the user's `onlyShowEventfullEvents` preference in the database.

### get-pinned-events.ts
Fetches pinned Eventfull events by ID from the EventfullEventModel, returning event IDs and names.

## google/

### create-google-calendar-event.ts
Creates an event in Google Calendar via the API, converts from unified format, and stores in the database.

### delete-google-calendar-event.ts
Deletes an event from Google Calendar and performs a hard delete from the database.

### get-google-calendar-events.ts
Fetches events from Google Calendar, converts to unified format, and syncs to the database.

### update-google-calendar-event.ts
Updates an existing Google Calendar event and syncs changes to the database.

## microsoft/

### create-microsoft-calendar-event.ts
Creates an event in Microsoft Calendar via Graph API, converts from unified format, and stores in the database.

### delete-microsoft-calendar-event.ts
Deletes an event from Microsoft Calendar and performs a hard delete from the database.

### get-microsoft-calendar-events.ts
Fetches events from Microsoft Calendar via Graph API, converts to unified format, and syncs to the database.

### update-microsoft-calendar-event.ts
Updates an existing Microsoft Calendar event via Graph API and syncs changes to the database.

## local-calendar/

### add-local-calendar-event.ts
Creates a local-only calendar event with a UUID, stored only in the app database (not synced to external calendars).

### delete-local-calendar-event.ts
Performs a soft delete of a local calendar event from the database.

### update-local-calendar-event.ts
Updates an existing local calendar event in the database.
