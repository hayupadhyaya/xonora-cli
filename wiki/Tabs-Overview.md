# Tabs Overview

The TUI has 9 tabs, switched with number keys `1`–`9`. The bottom status bar shows latency, audio state, and current keybinding hints.

## 1. Dashboard

At-a-glance view of connection health, latency, current player, audio output, top 5 players, playback state, and the **Built-In Test (BIT)** panel.

BIT live-monitors every subsystem across four categories:

- **CORE** — `core.initialized`, `core.audioPump`
- **NET** — `net.maWebSocket`, `net.sendspin`, `net.players`, `net.clockSync` (RTT and offset)
- **AUDIO** — `audio.queueRunning`, `audio.dataFlow`, `audio.streamFormat`
- **DATA** — `data.queueState`, `data.nowPlaying`, `data.playbackState`

Each check shows `+` (pass), `-` (fail), `!` (degraded) and a live status message.

## 2. Players

Lists every MA player on the server. Select one with `j` / `k` or arrows and press `Enter` to route playback to it. Shows player name, current track, and volume per player.

## 3. Queue

Full queue of the currently active player. Scroll with `j` / `k` or arrows, `Enter` to jump to an item.

## 4. Library

Browse your MA library across 7 categories:

- Albums, Artists, Tracks, Playlists, Podcasts, Audiobooks, Radios

Navigate subtabs with arrow keys; `Enter` opens the selected item.

## 5. Search

Global search across the library. An input field is always visible at the top — type your query and press `Enter`. Results are grouped by type (tracks, albums, artists, playlists).

## 6. Sendspin

Direct view into the Sendspin audio pipeline: current codec, sample rate, channels, bit depth, pre-decode buffer fill, clock sync state, and recent sendspin events. Includes a codec-switch control (FLAC / Opus / PCM) and a **test-all-codecs** mode for diagnosing which formats your server supports.

## 7. Party

Xonora's shared-listening mode. Runs in one of two roles:

- **Host** — start a party, share the Party URL / QR code, and other Xonora clients (iOS, Android, CLI guests) join and listen in sync.
- **Guest** — paste a Party URL to join an existing party as a listener.

## 8. Console

Interactive MA API console. A built-in registry of Music Assistant WebSocket commands (Auth, Players, Queues, Music, Providers, etc.) — browse with `Ctrl+B`, filter with `/`, hit `Enter` on a command to fill in args and run it. Responses render as pretty-printed JSON.

## 9. Logs

Live event log. Every MA event, Sendspin frame summary, audio pipeline state change, and error shown in real time. Use this tab first when diagnosing issues.
