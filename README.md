<p align="center">
  <img src="docs/images/logo.png" alt="Xonora" width="160"/>
</p>

<h1 align="center">xonora-cli</h1>

<p align="center">
  A native C++ terminal client for <a href="https://music-assistant.io/">Music Assistant</a>.<br/>
  Gapless, lossless, low-latency playback from your self-hosted MA server — straight from your terminal.
</p>

<p align="center">
  <a href="https://github.com/hayupadhyaya/xonora-cli/releases/latest"><img alt="Release" src="https://img.shields.io/github/v/release/hayupadhyaya/xonora-cli?include_prereleases"/></a>
  <img alt="Platform" src="https://img.shields.io/badge/platform-macOS%2013%2B-blue"/>
  <a href="https://discord.gg/x6cWh4AjNG"><img alt="Discord" src="https://img.shields.io/badge/discord-join-5865F2?logo=discord&logoColor=white"/></a>
</p>

---

## What is Xonora?

**Xonora** is a high-performance, native client suite for [Music Assistant](https://music-assistant.io/) — the self-hosted music server that unifies Spotify, Apple Music, Plex, Jellyfin, local libraries, and more behind one API. Xonora ships native apps for **iOS, watchOS, tvOS, CarPlay, Android**, and now a **C++ terminal CLI** for macOS.

All clients share a custom audio engine (**SendspinKit** on Apple platforms, **xonora-core** in C++) that delivers gapless, synchronized, lossless playback with NTP-style clock sync against your MA server.

## What is xonora-cli?

`xonora-cli` is the terminal client — a single self-contained executable that:

- Connects directly to your Music Assistant server over WebSocket
- Decodes FLAC / PCM / Opus streams natively and plays them through CoreAudio
- Renders a 9-tab full-screen TUI (FTXUI) with dashboard, library, queue, search, logs, and a built-in Party mode
- Supports multi-speaker control, clock-synchronized playback, and a Remote (WebRTC) mode for out-of-network access

No Electron, no web view, no background daemon — just a ~3 MB binary.

![Dashboard](docs/images/dashboard.png)

## Features

- **9-tab TUI** — Dashboard, Players, Queue, Library, Search, Sendspin, Party, Console, Logs
- **Native audio** — FLAC, PCM, Opus decoders feeding macOS AudioQueue at the stream's native sample rate
- **Gapless playback** with 5s pre-decode buffer and NTP-style clock sync
- **Built-In Test (BIT) panel** — live health checks of every subsystem
- **Multi-player control** — drive any MA player (phone, web, Sonos, etc.) from your terminal
- **Party mode** — take over remote players for a synchronized listening session
- **Remote mode (beta)** — WebRTC peer connection + DataChannels for access outside your LAN *(arm64 build only in v0.1)*

See the [Wiki](https://github.com/hayupadhyaya/xonora-cli/wiki) for full feature docs and keybindings.

## Requirements

- **macOS 13 (Ventura) or later**
- A reachable **Music Assistant** server (schema 28+) with the **Sendspin** provider enabled
- Terminal with true-color support (Terminal.app, iTerm2, Alacritty, kitty, WezTerm all work)

## Install

### Homebrew (recommended)

```sh
brew tap hayupadhyaya/xonora
brew install xonora-cli
```

### Manual download

Grab the binary for your Mac from [Releases](https://github.com/hayupadhyaya/xonora-cli/releases/latest):

- **Apple Silicon (M1/M2/M3/M4)** — `xonora-cli-vX.Y-macos-arm64.tar.gz`
- **Intel (x86_64)** — `xonora-cli-vX.Y-macos-x86_64.tar.gz`

```sh
# Example for Apple Silicon
curl -L -o xonora-cli.tar.gz https://github.com/hayupadhyaya/xonora-cli/releases/latest/download/xonora-cli-v0.1-macos-arm64.tar.gz
tar -xzf xonora-cli.tar.gz
chmod +x xonora-cli
sudo mv xonora-cli /usr/local/bin/   # or /opt/homebrew/bin on Apple Silicon
```

On first launch, macOS Gatekeeper may block the unsigned binary. Allow it via **System Settings → Privacy & Security → "Open Anyway"**, or run once with:

```sh
xattr -d com.apple.quarantine /opt/homebrew/bin/xonora-cli
```

### Coming soon

- **Intel Mac x86_64** — shipped from v0.1 (local mode only, no Remote/WebRTC)
- **Linux (x86_64, arm64)** — planned for v0.2
- **Windows (x86_64)** — planned for v0.3

## Quick start

```sh
xonora-cli                              # auto-discover MA server on your LAN
xonora-cli --server 192.168.1.50:8095   # explicit server
xonora-cli --player "Living Room"       # pick a specific MA player
xonora-cli --help                       # all flags
```

Inside the TUI:

| Key       | Action                    |
|-----------|---------------------------|
| `1`–`9`   | Switch tabs               |
| `Space`   | Play / Pause              |
| `[` / `]` | Previous / Next track     |
| `A`       | Toggle local audio output |
| `q`       | Quit                      |

Full keybinding reference: [Wiki → Keybindings](https://github.com/hayupadhyaya/xonora-cli/wiki/Keybindings).

## Known issues (v0.1)

- **PCM & Opus silent** — only FLAC currently produces audio. PCM fallback (bit_depth=0→16) landed; Opus decoder configure may fail on some servers. Use FLAC output format in MA until fixed.
- **Remote (WebRTC) mode unverified** — the WebRTC signalling + DTLS-pinned DataChannels compile and connect, but end-to-end playback over remote hasn't been fully validated in real-world NAT conditions. Needs field testing.
- **Intel x86_64 build has no Remote mode** — cross-compile limitation on the v0.1 build host. Apple Silicon users get the full feature set.
- **Dashboard queue/playback panel** — some MA event types update the Logs tab but do not refresh the Dashboard summary until a full event cycle passes.

See [Wiki → Troubleshooting](https://github.com/hayupadhyaya/xonora-cli/wiki/Troubleshooting) for workarounds.

## License

**Proprietary & closed-source.** The `xonora-cli` binary is distributed free of charge for personal, non-commercial use with Music Assistant. Source code is not publicly available. No warranty. All rights reserved © Hay Upadhyaya.

## Third-party dependencies

`xonora-cli` statically links the following open-source libraries. Full license texts are bundled inside the release tarball under `licenses/`.

| Library | Version | License | Purpose |
|---------|---------|---------|---------|
| [FTXUI](https://github.com/ArthurSonzogni/FTXUI) | 5.0.0 | MIT | Terminal UI |
| [IXWebSocket](https://github.com/machinezone/IXWebSocket) | 11.4.5 | BSD-3-Clause | WebSocket client |
| [libFLAC](https://github.com/xiph/flac) | 1.4.3 | BSD-3-Clause (Xiph) | FLAC decode |
| [libopus](https://github.com/xiph/opus) | 1.5.2 | BSD-3-Clause (Xiph) | Opus decode |
| [libdatachannel](https://github.com/paullouisageneau/libdatachannel) | 0.22.x | MPL-2.0 | WebRTC DataChannels (Remote mode) |
| [libjuice](https://github.com/paullouisageneau/libjuice) | bundled | MPL-2.0 | ICE for WebRTC |
| [usrsctp](https://github.com/sctplab/usrsctp) | bundled | BSD-3-Clause | SCTP for DataChannels |
| [nlohmann/json](https://github.com/nlohmann/json) | 3.11.3 | MIT | JSON parsing |
| [qrcodegen](https://github.com/nayuki/QR-Code-generator) | 1.8.0 | MIT | QR code rendering (Remote pairing) |
| Apple AudioToolbox / CoreAudio | — | Apple SDK | Audio output |

## Community & support

- **Discord** — <https://discord.gg/x6cWh4AjNG>
- **Issues** — <https://github.com/hayupadhyaya/xonora-cli/issues>
- **Music Assistant project** — <https://music-assistant.io/>

---

<p align="center">Developed by Hay Upadhyaya. Not affiliated with Music Assistant or any streaming service.</p>
