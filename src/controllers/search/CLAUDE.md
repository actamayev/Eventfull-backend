# Search Directory

Controllers for search functionality. Both endpoints filter out blocked users and limit results to 10.

## Files

### search-for-event.ts
Searches events by name using case-insensitive regex. Returns active events excluding those from blocked users, with event status (past/ongoing/upcoming) calculated via `determineEventStatus`.

### search-for-username.ts
Searches users by username using case-insensitive regex. Excludes blocked users and the requesting user. Returns user IDs and usernames.
