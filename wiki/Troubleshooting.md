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

## Known issues (v0.1)

### PCM and Opus streams are silent

Only **FLAC** produces audio in v0.1. Workaround: in the MA UI, set the stream output format to FLAC for the target player.

- PCM with `bit_depth=0` in the stream header now falls back to 16-bit, but some servers still emit empty decode buffers.
- Opus decoder `configure()` may fail on some stream/start headers; the Logs tab will show `decoder->configure() FAILED` when this happens.

### Remote (WebRTC) mode unverified

Signalling and DTLS connect, but real-world NAT-traversed playback hasn't been confirmed end-to-end. If it works for you, please report to Discord so we can close this out.

### Intel (x86_64) build has no Remote mode

The v0.1 x86_64 binary was cross-compiled from Apple Silicon without the WebRTC stack. Use the arm64 build for remote mode, or wait for v0.2.

### Dashboard queue/playback panel lags

Some MA event types land in the Logs tab but do not immediately refresh the Dashboard summary. A new track or playback event typically refreshes it within a cycle.

## Common fixes

### Gatekeeper blocks the binary

```sh
xattr -d com.apple.quarantine $(which xonora-cli)
```

Or approve in **System Settings → Privacy & Security → Open Anyway**.

### Connecting to a server for the first time

Pass the server URL and credentials explicitly. These are saved to `~/.xonora-cli/config.json` after a successful connection:

```sh
xonora-cli --server ws://<MA-IP>:8095 --user <username> --pass <password>
# or with a token
xonora-cli --server ws://<MA-IP>:8095 --token <token>
```

Subsequent runs can use `xonora-cli` alone to reuse saved credentials.

### "Sendspin connection failed"

Verify the **Sendspin** player provider is installed and enabled on your MA server. `xonora-cli` requires Sendspin for audio delivery.

### Audio starts mid-track or ends early

Fixed in v0.1 via pipeline-side rate limiting. If you still see it, capture logs (`2>/tmp/xonora.log`) and share the `AudioPipeline OUT` lines on Discord.

### Terminal renders garbled / no color

Ensure `TERM=xterm-256color` or `TERM=screen-256color`. tmux users may need `tmux -2` or `set -g default-terminal "tmux-256color"` in `~/.tmux.conf`.

## Getting help

- **Discord** — <https://discord.gg/x6cWh4AjNG> (fastest)
- **Issues** — <https://github.com/hayupadhyaya/xonora-cli/issues>

When reporting an issue, please include:

1. macOS version and architecture (`uname -m`)
2. `xonora-cli --help` output (confirms binary version)
3. `/tmp/xonora.log` output covering the issue
4. Relevant lines from the in-TUI Logs tab (`9`)
