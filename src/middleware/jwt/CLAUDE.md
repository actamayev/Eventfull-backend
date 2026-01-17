# JWT Directory
Express and Socket.io middleware for JWT authentication and authorization.

## Files

### jwt-verify.ts
Express middleware that authenticates regular users. Validates the authorization header, decodes the JWT to extract userId, fetches the user from DB, and attaches it to `req.user`. Returns 401 on failure.

### admin-jwt-verify.ts
Express middleware that authenticates admin users. Same flow as jwt-verify but uses admin-specific decoder and lookup, attaching the admin to `req.admin`.

### verify-socket-jwt.ts
Socket.io middleware for WebSocket authentication. Extracts accessToken from handshake query params, decodes userId, and attaches it to `socket.userId`. Passes an Error to next() on failure.
