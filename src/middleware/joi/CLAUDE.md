# Joi Directory
Joi validation schemas for event-related request/response validation.

## Files

### new-eventfull-event-schema.ts
Validates new Eventfull event creation requests. Defines schemas for event times (singular, ongoing, custom) and the complete new event payload including name, price, type, frequency, address, invitees, and co-hosts.

### unified-calendar-event-schema.ts
Validates external calendar events (Google/Outlook). Provides `createFullUnifiedCalendarEventSchema` for complete calendar events with source-specific validation, and `partialUnifiedCalendarEventSchema` for events without id/source fields.

### updated-eventfull-event-schema.ts
Validates existing Eventfull event updates. Extends the new event schema with additional fields: `_id`, `__v`, `eventImages`, `attendees`, `createdBy`, and timestamps. Also exports `socialDataSchema` used by other schemas.
