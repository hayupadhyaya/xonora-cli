# Tabs Overview

The TUI has 9 tabs, switched with number keys `1`–`9`. The bottom status bar shows latency, audio state, and current keybinding hints.

## 1. Dashboard

At-a-glance view of connection health, latency, current player, audio output, top 5 players, playback state, and the **Built-In Test (BIT)** panel.

BIT live-monitors every subsystem:

- **CORE** — singleton init, audio pump
- **NET** — MA WebSocket, Sendspin, player registration, clock sync (RTT and offset)
- **AUDIO** — AudioQueue state, data flow, stream format
- **DATA** — queue state, now-playing, playback state events

## 2. Players

Lists every MA player on the server. Select one and press `Enter` to route playback to it. Shows track, progress, time, and volume per player.

## 3. Queue

Full queue of the currently active player. Scroll with `j`/`k` or arrow keys, `Enter` to jump to an item.

## 4. Library

Browse your MA library. Subtabs for Albums, Artists, Tracks, Playlists, Podcasts, Radios, Audiobooks. Press `/` to search within the current subtab.

## 5. Search

Global search across the library. Results grouped by type (tracks, albums, artists, playlists).

## 6. Sendspin

Direct view into the Sendspin audio pipeline: codec, sample rate, channels, bit depth, pre-decode buffer fill, output ring fill, clock sync RTT/offset.

## 7. Party

Party mode lets you take over one or more remote MA players and drive synchronized playback from the CLI. Select players to enlist, then play normally — all enlisted players follow.

## 8. Console

Interactive MA command console. Type MA JSON-RPC commands directly and see responses. Useful for debugging MA integrations.

## 9. Logs

Live event log. Every MA event, Sendspin frame, audio pipeline state change, and error is shown here in real time. Use this tab first when diagnosing issues.
