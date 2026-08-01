---
name: Pair a playback device to a sound zone
description: Initiate pairing and bind a device to a Soundtrack sound zone.
api: graphql/soundtrack-your-brand.graphql
endpoint: https://api.soundtrackyourbrand.com/v2
operations: [soundZoneInitiatePairing, soundZonePairDevice, devicePair, soundZoneUnpair, device]
---

# Pair a playback device to a sound zone

Bind a hardware/app player to a sound zone so it can play the zone's music.

## Auth
`Authorization: Basic <api_token>` or a user `Bearer` token
(`authentication/soundtrack-your-brand-authentication.yml`).

## Steps
1. Start pairing for the zone with **`soundZoneInitiatePairing(input: { soundZone: $id })`**
   (or **`devicePair`** from the device side to obtain/consume a pairing code).
2. Bind the device with **`soundZonePairDevice(input: { soundZone: $id, device: $deviceId })`**.
3. Verify with `device(id: $deviceId)` / `soundZone(id: $id)`.
4. To release, call **`soundZoneUnpair(input: { soundZone: $id })`**.

## Notes
- Confirm the zone and device ids first — pairing changes where audio physically plays.
- GraphQL errors arrive in `errors[]`; refresh on HTTP 401 with `refreshLogin`.
