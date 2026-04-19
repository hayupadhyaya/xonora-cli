# Troubleshooting

## Capturing logs

The TUI hides `stderr`. To capture full diagnostic output, redirect it to a file:

```sh
xonora-cli 2>/tmp/xonora.log
```

In another terminal, tail the file:

```sh
tail -f /tmp/xonora.log
```

Filter for the interesting bits:

```sh
grep -E "AudioPipeline|AUD|pump:" /tmp/xonora.log
```

The in-TUI **Logs tab** (press `9`) shows the high-level event log. `/tmp/xonora.log` shows the raw engine output (decoder state, pipeline drains, ring-buffer fills).

## Known issues (v0.3.10)

### Remote (WebRTC) mode is experimental

`--webrtc CODE` ships on every platform in v0.3.10 and works in local testing, but has not been validated across the full range of real-world NAT / firewall topologies. If it misbehaves on your setup, please file an issue with your network details and Logs tab output.

### Party mode is experimental

Hosting and joining shared listening sessions works in local testing, but is not yet broadly validated across multiple devices. Feedback from multi-device testers is welcome on Discord.

### Multi-player cross-device sync can drift

Group playback is clock-synced, but peers on different devices may still be audibly a few milliseconds off after extended play. Refinements are tracked for a follow-up release.

### Dashboard refresh lag on some MA events

Some MA event types land in the Logs tab but do not immediately refresh the Dashboard summary. A new track or playback event typically refreshes it within a cycle.

### WSL2 has no local audio

WSL2 doesn't expose an audio device to Linux binaries, so the Linux build inside WSL2 runs as a **remote controller only**. Use the native Windows `.zip` (WASAPI) for local audio on Windows.

## Common fixes

### Gatekeeper blocks the binary

```sh
xattr -d com.apple.quarantine $(which xonora-cli)
```

Or approve in **System Settings → Privacy & Security → Open Anyway**.

### Connecting to a server for the first time

Pass the server URL and credentials explicitly. These are saved to the OS-standard config path (`~/Library/Application Support/xonora/config.json` on macOS, `~/.config/xonora/config.json` on Linux, `%APPDATA%\xonora\config.json` on Windows) after a successful connection:

```sh
xonora-cli --server ws://<MA-IP>:8095 --user <username> --pass <password>
# or with a token
xonora-cli --server ws://<MA-IP>:8095 --token <token>
```

Subsequent runs can use `xonora-cli` alone to reuse saved credentials.

### "Sendspin connection failed"

Verify the **Sendspin** player provider is installed and enabled on your MA server. `xonora-cli` requires Sendspin for audio delivery.

### Audio starts mid-track or ends early

Fixed in v0.3.x via pipeline-side rate limiting and unified clock-domain scheduling. If you still see it, capture logs (`2>/tmp/xonora.log`) and share the `AudioPipeline OUT` lines on Discord.

### Terminal renders garbled / no color

Ensure `TERM=xterm-256color` or `TERM=screen-256color`. tmux users may need `tmux -2` or `set -g default-terminal "tmux-256color"` in `~/.tmux.conf`.

## Getting help

- **Discord** — <https://discord.gg/x6cWh4AjNG> (fastest)
- **Issues** — <https://github.com/hayupadhyaya/xonora-cli/issues>

When reporting an issue, please include:

1. OS and architecture (macOS arm64, Linux x86_64 / arm64, Windows x86_64)
2. `xonora-cli --version` output (confirms binary version and whether `+webrtc` is compiled in)
3. `/tmp/xonora.log` output covering the issue (or `%TEMP%\xonora.log` on Windows)
4. Relevant lines from the in-TUI Logs tab (`9`)
