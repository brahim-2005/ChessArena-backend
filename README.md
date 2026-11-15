# ChessArena Backend Source

This repository organizes the current ChessArena API route and server-side
source files:

- `src/app/api/` — Next.js route handlers for games, matchmaking, invitations,
  player search, and puzzle operations.
- `src/lib/supabase/` — server and admin Supabase clients.
- `src/lib/chess/` — server-side puzzle validation.
- `server/socket.js` — the existing isolated Socket.IO process.

## Important integration status

These API handlers use Next.js App Router, Next request/response types, and
Next.js cookie handling. The production web application still runs the
authoritative route handlers from its own `src/app/api` directory; this
repository is a source extract and is **not wired to the frontend as a
separately deployed backend**. The Socket.IO process is separate and is not
the durable game transport.

Do not deploy the Socket.IO service as production matchmaking. Separating the
API service requires configuring cross-origin requests, Supabase cookie/session
handling, and the frontend API base URL, then validating those flows.

## Required environment

Copy `.env.example` to `.env.local` and supply values from your own Supabase
project. Keep the service-role key server-only and do not commit `.env.local`.
Database schema setup is maintained in `ChessArena-database`.
