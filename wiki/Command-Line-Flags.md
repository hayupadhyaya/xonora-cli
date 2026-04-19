# Command-Line Flags

```
xonora-cli [options]
```

`xonora-cli` supports two connection modes. Pass one of:

## Direct mode (LAN or reverse proxy)

| Flag | Description |
|------|-------------|
| `--server URL` | Music Assistant server URL (`ws://` or `http://`) |
| `--sendspin URL` | Sendspin server URL (default: derived from `--server`) |
| `--token TOKEN` | Access token authentication |
| `--user USER` | Username (combine with `--pass`) |
| `--pass PASS` | Password |

Example:
```sh
xonora-cli --server ws://192.168.1.50:8095 --token abcdef123456
```

## Remote mode (WebRTC via signalling server)

| Flag | Description |
|------|-------------|
| `--webrtc [CODE]` | 26-char Remote ID from <https://app.music-assistant.io>. Dashes optional. Omit `CODE` to reuse the last-saved Remote ID. |
| `--signaling URL` | Signalling server (default: `wss://signaling.music-assistant.io/ws`) |

Example:
```sh
xonora-cli --webrtc XXXXXXXX-XXXXX-XXXXX-XXXXXXXX
```

`--webrtc` is mutually exclusive with the direct-mode flags. Remote mode authenticates via DTLS certificate pinning derived from the Remote ID, so no separate credentials are required. See [Remote Mode](Remote-Mode) for setup details.

## Common options

| Flag | Description |
|------|-------------|
| `--name NAME` | Player display name shown in MA (default: `Xonora CLI`) |
| `--audio` | Enable local audio output on launch (default: off) |
| `--force-codec {flac,opus,pcm}` | Override MA's codec negotiation for this session |
| `--version`, `-v` | Print binary version (and `+webrtc` tag if remote transport is compiled in) and exit |
| `--help`, `-h` | Show help and exit |

## Configuration persistence

Connection settings are saved on first successful connection:

- **macOS:** `~/Library/Application Support/xonora/config.json`
- **Linux:** `$XDG_CONFIG_HOME/xonora/config.json` (or `~/.config/xonora/config.json`)
- **Windows:** `%APPDATA%\xonora\config.json`

Running `xonora-cli` with no arguments reuses the saved direct-mode server. To switch to remote mode, pass `--webrtc` with a new Remote ID (or `--webrtc` alone to reuse the saved ID).
