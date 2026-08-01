---
name: Show what's playing in a sound zone
description: Read the current track in a Soundtrack sound zone and keep it live.
api: graphql/soundtrack-your-brand.graphql
endpoint: https://api.soundtrackyourbrand.com/v2
operations: [nowPlaying, nowPlayingUpdate, soundZone]
---

# Show what's playing in a sound zone

Use the Soundtrack GraphQL API to display and live-update the current track for a
store's sound zone.

## Auth
Send `Authorization: Basic <api_token>` (API client token) or `Authorization: Bearer <token>`
(user token from `loginUser`). See `authentication/soundtrack-your-brand-authentication.yml`.

## Steps
1. Resolve the sound zone id you care about — from `account { soundZones { edges { node { id name } } } }`
   (Relay cursor pagination, see `conventions/soundtrack-your-brand-conventions.yml`).
2. Query **`nowPlaying(soundZone: $id)`** for `track { name artists { name } album { image { url } } }`.
3. For a live display, open a websocket subscription to **`nowPlayingUpdate`** for the same zone
   (token as a query parameter) and re-render on each event.

## Notes
- GraphQL returns HTTP 200 with an `errors[]` array on failure; on HTTP 401 refresh via `refreshLogin`.
- Request only the fields you need — that is the point of GraphQL here.
