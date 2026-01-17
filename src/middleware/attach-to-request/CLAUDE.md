# Attach To Request Directory
Express middleware functions that fetch entities from the database and attach them to the request object for use in downstream handlers.

## Files

### attach-event-to-request.ts
Fetches an event by `eventfullEventId` from request body and attaches it to `req.event`. Returns 400 if event not found.

### attach-event-organizer-to-request.ts
Fetches the organizer user from `req.event.organizer.userId` and attaches it to `req.eventOrganizer`. Requires `attach-event-to-request` to run first. Returns 400 if organizer not found.
