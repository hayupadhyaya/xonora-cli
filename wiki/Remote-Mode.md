# Remote Mode (WebRTC)

Remote mode lets `xonora-cli` connect to your Music Assistant server from outside your LAN, without VPN, port forwarding, or a public IP — using WebRTC peer-to-peer with NAT traversal via ICE.

**Status in v0.3.10: experimental, needs testers.** The transport compiles and connects, and audio has been verified in local NAT setups, but end-to-end playback across real-world NAT / firewall topologies has not been broadly validated. Please report results on the Discord or GitHub Issues.

**Availability:** all platforms in v0.3.10 ship WebRTC — macOS arm64, Linux x86_64/arm64, and Windows x86_64 binaries all include the remote transport. Run `xonora-cli --version` and look for the `+webrtc` tag to confirm.

## How it works

1. You generate a **Remote ID** (26-char code) from <https://app.music-assistant.io> — this is a public-key fingerprint tied to a DTLS certificate on the MA side.
2. Both peers connect to a **signalling server** (WSS) to exchange SDP offer/answer and ICE candidates.
3. A direct WebRTC `PeerConnection` is established, and two ordered/reliable DataChannels open:
   - `ma-api` — relays the Music Assistant JSON-RPC WebSocket traffic
   - `sendspin` — relays the Sendspin binary audio protocol (framing preserved)
4. DTLS pins the Remote ID fingerprint, so no man-in-the-middle attack can impersonate your server. This authenticates the **transport**, not your Music Assistant session.

The Remote ID secures the tunnel. Your MA server still enforces its own auth: if your server has a username/password configured, you'll be prompted to sign in after the tunnel comes up, exactly like a direct connection.

**v0.3.10 limitation:** the CLI currently rejects `--webrtc` combined with `--user` / `--pass` / `--token`. If your MA server requires auth, you'll see an "Authentication required" error on the Dashboard after the WebRTC transport connects. This is tracked for v0.3.11. Workarounds today: use a passwordless MA setup for WebRTC testing, or fall back to direct mode with `--user` / `--pass` over LAN / reverse proxy.

## Using it

```sh
# First time — pass the Remote ID
xonora-cli --webrtc XXXXXXXX-XXXXX-XXXXX-XXXXXXXX

# Reuse the saved Remote ID
xonora-cli --webrtc

# Custom signalling server (rare)
xonora-cli --webrtc XXXXXXXX-... --signaling wss://your.signaling.example.com/ws
```

Dashes in the Remote ID are optional — the CLI strips them before parsing.

## Limitations

- One MA server per Remote ID. To switch servers, pass a new Remote ID.
- Signalling-server reachability is required to establish the connection. Once connected, audio flows peer-to-peer.
- Some symmetric-NAT environments may require a TURN relay, which the default signalling server does not currently provide.
- Audio over WebRTC uses the same codecs as direct mode (FLAC / PCM / Opus) — the data flows unchanged through the `sendspin` DataChannel.

## Troubleshooting

- **"No Remote ID" error** — run with `--webrtc CODE` once; subsequent runs can use `--webrtc` alone.
- **Connection never opens** — check the Logs tab for signalling errors. The signalling server must be reachable; test with `wscat -c wss://signaling.music-assistant.io/ws`.
- **Connects but no audio** — most commonly a codec negotiation issue across the relay. Try `--force-codec flac`, and share the Logs tab output on Discord or in a GitHub issue if it persists.
