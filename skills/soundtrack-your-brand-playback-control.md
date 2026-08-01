---
name: Control playback in a sound zone
description: Play, pause, skip and set volume for a Soundtrack sound zone.
api: graphql/soundtrack-your-brand.graphql
endpoint: https://api.soundtrackyourbrand.com/v2
operations: [play, pause, skipTrack, setVolume, soundZone, playbackUpdate]
---

# Control playback in a sound zone

Drive real-time playback controls for a store's sound zone.

## Auth
`Authorization: Basic <api_token>` or a user `Bearer` token
(`authentication/soundtrack-your-brand-authentication.yml`).

## Steps
1. Get the target sound zone id (`soundZone(id: ...)` or via `account { soundZones }`).
2. Control playback with the mutations:
   - **`play(input: { soundZone: $id })`** / **`pause(input: { soundZone: $id })`**
   - **`skipTrack(input: { soundZone: $id })`** to advance
   - **`setVolume(input: { soundZone: $id, volume: $level })`** to adjust volume
3. Confirm state by subscribing to **`playbackUpdate`** (or re-query `nowPlaying`).

## Notes
- These are control-plane actions on a physical zone — treat them as consequential; verify the
  correct `soundZone` id before issuing.
- On `errors[]` inspect `message`/`path`; on HTTP 401 refresh the token via `refreshLogin`.
