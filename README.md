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
  <img alt="Platform" src="https://img.shields.io/badge/platform-macOS%20%7C%20Linux%20%7C%20Windows-blue"/>
  <a href="https://discord.gg/x6cWh4AjNG"><img alt="Discord" src="https://img.shields.io/badge/discord-join-5865F2?logo=discord&logoColor=white"/></a>
</p>

---

## What is Xonora?

**Xonora** is a high-performance, native client suite for [Music Assistant](https://music-assistant.io/) — the self-hosted music server that unifies Spotify, Apple Music, Plex, Jellyfin, local libraries, and more behind one API. Xonora ships native apps for **iOS, watchOS, and CarPlay**, and a **cross-platform C++ terminal CLI** with native binaries for macOS (Apple Silicon), Linux (x86_64 + arm64), and Windows (x86_64). Android and tvOS clients are in development.

All clients share a custom audio engine (**SendspinKit** on Apple platforms, **xonora-core** in C++) that delivers gapless, synchronized, lossless playback with NTP-style clock sync against your MA server.

## What is xonora-cli?

`xonora-cli` is the terminal client — a single self-contained executable that:

- Connects directly to your Music Assistant server over WebSocket
- Decodes FLAC / PCM / Opus streams natively and plays them through the OS audio stack (CoreAudio / ALSA / WASAPI via [miniaudio](https://miniaud.io/))
- Renders a full-screen TUI (FTXUI) with dashboard, library, queue, search, logs, and a built-in Party mode
- Supports multi-speaker control and clock-synchronized playback

No Electron, no web view, no background daemon — just a ~5 MB binary.

![Dashboard](docs/images/dashboard.png)

## Supported Platforms          

<!-- BEGIN:PLATFORMS -->
- **macOS** arm64 (Apple Silicon) — macOS 12 (Monterey) or newer; full local audio via CoreAudio. Intel Macs are not supported in v0.3.10.
- **Linux** x86_64, arm64 — Fedora, Ubuntu 22.04+, Debian 12+, Arch, RHEL 8+ (glibc 2.28+); full local audio via ALSA
- **Windows** x86_64 — Windows 10 or newer; full local audio via WASAPI (native build). WSL2 is also supported as a remote-control-only fallback.
<!-- END:PLATFORMS -->                                                                                                              

## Features

- **9-tab TUI** — Dashboard, Players, Queue, Library, Search, Sendspin, Party, Console, Logs
- **Native audio** — FLAC, PCM, Opus decoders feeding the OS audio stack (miniaudio: CoreAudio / ALSA / WASAPI) at the stream's native sample rate
- **Cross-platform** — single codebase builds for macOS (arm64), Linux (x86_64 + arm64), and Windows (x86_64, native)
- **Gapless playback** with 5s pre-decode buffer and NTP-style clock sync
- **Built-In Test (BIT) panel** — live health checks across CORE, NET, AUDIO, DATA subsystems
- **Multi-player control** — drive any MA player (phone, web, Sonos, etc.) from your terminal
- **Party mode** — host or join a shared listening session with other Xonora clients

See the [Wiki](https://github.com/hayupadhyaya/xonora-cli/wiki) for full feature docs and keybindings.

## Requirements

- **macOS 12 (Monterey) or later** (Apple Silicon only — Intel macOS not supported in v0.3.10), **Linux** (glibc 2.28+ — Fedora, Ubuntu 22.04+, Debian 12+, Arch, RHEL 8+), or **Windows 10 or newer** (x86_64, native)
- A reachable **Music Assistant** server (schema 28+) with the **Sendspin** provider enabled
- Terminal with true-color support (Terminal.app, iTerm2, Alacritty, kitty, WezTerm, Windows Terminal all work)
- Linux: ALSA runtime — `libasound2t64` (Ubuntu 24.04+), `libasound2` (Ubuntu 22.04 / Debian 12), `alsa-lib` (Fedora / Arch). Pre-installed on most desktop distros.

## Installation           
                                                                                                                                      
<!-- BEGIN:INSTALL -->
### macOS (Apple Silicon)

Homebrew:

```bash
brew install hayupadhyaya/xonora/xonora-cli
```

Or download directly:

```bash
curl -L -o xonora-cli.tar.gz \
  https://github.com/hayupadhyaya/xonora-cli/releases/download/cli-v0.3.10/xonora-cli-v0.3.10-macos-arm64.tar.gz
tar -xzf xonora-cli.tar.gz && sudo mv xonora-cli-v0.3.10-macos-arm64/xonora-cli /usr/local/bin/
```

Intel Macs: not supported in v0.3.10 — Apple Silicon only.

### Linux

Install the ALSA runtime (one-time). **Note:** Ubuntu renamed the package from `libasound2` to `libasound2t64` starting in 24.04 (part of the `time_t` 64-bit transition) — on 24.04+ the old name has no install candidate, use `libasound2t64`:

```bash
# Ubuntu 24.04+ / Debian trixie (package renamed)
sudo apt install -y libasound2t64
# Ubuntu 22.04 / Debian 12 (old name)
sudo apt install -y libasound2
# Fedora / RHEL
sudo dnf install -y alsa-lib
# Arch
sudo pacman -S --needed alsa-lib
```

Then download the binary:

```bash
ARCH=$(uname -m); [ "$ARCH" = "aarch64" ] && ARCH=arm64
curl -L -o xonora-cli.tar.gz \
  https://github.com/hayupadhyaya/xonora-cli/releases/download/cli-v0.3.10/xonora-cli-v0.3.10-linux-${ARCH}.tar.gz
tar -xzf xonora-cli.tar.gz && sudo mv xonora-cli-v0.3.10-linux-${ARCH}/xonora-cli /usr/local/bin/
```

### Windows

Download [`xonora-cli-v0.3.10-windows-x86_64.zip`](https://github.com/hayupadhyaya/xonora-cli/releases/download/cli-v0.3.10/xonora-cli-v0.3.10-windows-x86_64.zip), extract it, and run `xonora-cli.exe`. No dependencies required — audio plays through WASAPI via the OS.

```powershell
# PowerShell
Invoke-WebRequest -Uri "https://github.com/hayupadhyaya/xonora-cli/releases/download/cli-v0.3.10/xonora-cli-v0.3.10-windows-x86_64.zip" -OutFile xonora-cli.zip
Expand-Archive xonora-cli.zip -DestinationPath .
.\xonora-cli-v0.3.10-windows-x86_64\xonora-cli.exe --help
```

WSL2 is also supported, but runs in **remote-control mode only** — WSL2 doesn't expose an audio device to Linux binaries. For local audio, use the native `.zip` above. For remote control only, install [WSL2](https://learn.microsoft.com/en-us/windows/wsl/install) with Ubuntu and follow the Linux x86_64 instructions (do **not** press `A` / pass `--audio`).
<!-- END:INSTALL -->  

## Downloads                           
                                       
<!-- BEGIN:DOWNLOADS -->
Latest release: **v0.3.10** — [release notes](https://github.com/hayupadhyaya/xonora-cli/releases/tag/cli-v0.3.10)

| Platform | Architecture | Download |
|----------|--------------|----------|
| macOS | arm64 (Apple Silicon) | [xonora-cli-v0.3.10-macos-arm64.tar.gz](https://github.com/hayupadhyaya/xonora-cli/releases/download/cli-v0.3.10/xonora-cli-v0.3.10-macos-arm64.tar.gz) |
| Linux | x86_64 | [xonora-cli-v0.3.10-linux-x86_64.tar.gz](https://github.com/hayupadhyaya/xonora-cli/releases/download/cli-v0.3.10/xonora-cli-v0.3.10-linux-x86_64.tar.gz) |
| Linux | arm64 | [xonora-cli-v0.3.10-linux-arm64.tar.gz](https://github.com/hayupadhyaya/xonora-cli/releases/download/cli-v0.3.10/xonora-cli-v0.3.10-linux-arm64.tar.gz) |
| Windows | x86_64 | [xonora-cli-v0.3.10-windows-x86_64.zip](https://github.com/hayupadhyaya/xonora-cli/releases/download/cli-v0.3.10/xonora-cli-v0.3.10-windows-x86_64.zip) |
| Checksums | all | [SHA256SUMS](https://github.com/hayupadhyaya/xonora-cli/releases/download/cli-v0.3.10/SHA256SUMS) |
<!-- END:DOWNLOADS -->  

### Roadmap

- **Multi-player sync refinement** — clock-synced group playback is live, but cross-device drift can still be audible on peers with divergent system clocks. Tightening filter convergence is the next focus.
- **WebRTC remote mode validation** — WebRTC (`--webrtc CODE`) ships in every release but has not been validated across real-world NAT / firewall topologies. Feedback from testers wanted.
- **Party mode validation** — hosting and joining a shared listening session works in local testing but hasn't been broadly validated. Feedback from testers wanted.
- **Homebrew tap** — published alongside this release.

## Quick start

First run (credentials are saved to the OS-standard config path: `~/Library/Application Support/xonora/config.json` on macOS, `~/.config/xonora/config.json` on Linux):

```sh
xonora-cli --server ws://192.168.1.50:8095 --user USERNAME --pass PASSWORD
# or with a token
xonora-cli --server ws://192.168.1.50:8095 --token YOUR_TOKEN
```

Subsequent runs:

```sh
xonora-cli                              # reuse saved server + credentials
xonora-cli --name "Kitchen Mac"         # override CLI's display name in MA
xonora-cli --audio                      # enable local audio on launch
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

## Known issues (v0.3.10)

- **Multi-player cross-device sync can drift** — group playback is clock-synced, but peers on different devices may still be audibly a few milliseconds off after extended play. Refinements are tracked for a follow-up release.
- **WebRTC remote mode is experimental** — `--webrtc CODE` ships in every binary and works in local testing, but has not been validated across real-world NAT / firewall topologies. Please file an issue with your network setup if it misbehaves.
- **Party mode is experimental** — hosting and joining a shared listening session works in local testing but is not yet broadly validated. Feedback from multi-device testers is welcome.
- **Dashboard refresh lag on some MA events** — a handful of MA event types update the Logs tab but may take a full event cycle to refresh the Dashboard summary panel.
- **WSL2 has no local audio** — WSL2 doesn't expose an audio device to Linux binaries, so the Linux build inside WSL2 runs as a **remote controller only**. Use the native Windows `.zip` (WASAPI) for local audio on Windows.

See [Wiki → Troubleshooting](https://github.com/hayupadhyaya/xonora-cli/wiki/Troubleshooting) for workarounds.

## License

**Proprietary & closed-source.** The `xonora-cli` binary is distributed free of charge for personal, non-commercial use with Music Assistant. Source code is not publicly available. No warranty. All rights reserved © Hay Upadhyaya.

## Third-party dependencies

`xonora-cli` statically links the following open-source libraries. Full license texts are bundled inside the release tarball under `licenses/`.

| Library | Version | License | Purpose |
|---------|---------|---------|---------|
| [FTXUI](https://github.com/ArthurSonzogni/FTXUI) | 5.0.0 | MIT | Terminal UI |
| [IXWebSocket](https://github.com/machinezone/IXWebSocket) | 11.4.6 | BSD-3-Clause | WebSocket client |
| [miniaudio](https://miniaud.io/) | 0.11.21 | MIT-0 / Public domain | Cross-platform audio output |
| [libFLAC](https://github.com/xiph/flac) | 1.4.3 | BSD-3-Clause (Xiph) | FLAC decode |
| [libopus](https://github.com/xiph/opus) | 1.5.2 | BSD-3-Clause (Xiph) | Opus decode |
| [nlohmann/json](https://github.com/nlohmann/json) | 3.11.3 | MIT | JSON parsing |
| [qrcodegen](https://github.com/nayuki/QR-Code-generator) | 1.8.0 | MIT | QR code rendering |

## Community & support

- **Discord** — <https://discord.gg/x6cWh4AjNG>
- **Issues** — <https://github.com/hayupadhyaya/xonora-cli/issues>
- **Music Assistant project** — <https://music-assistant.io/>

---

<p align="center">Developed by Hay Upadhyaya. Not affiliated with Music Assistant or any streaming service.</p>
