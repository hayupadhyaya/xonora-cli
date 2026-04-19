# Supported Platforms

- **macOS** arm64 (Apple Silicon) — macOS 12 (Monterey) or newer; full local audio via CoreAudio. Intel Macs are not supported in v0.3.10.
- **Linux** x86_64, arm64 — Fedora, Ubuntu 22.04+, Debian 12+, Arch, RHEL 8+ (glibc 2.28+); full local audio via ALSA
- **Windows** x86_64 — Windows 10 or newer; full local audio via WASAPI (native build). WSL2 is also supported as a remote-control-only fallback.

## Requirements

All platforms require:

- A [Music Assistant](https://music-assistant.io/) server (schema 28+) reachable on the network
- The **Sendspin** player provider enabled on the MA server
- A terminal with true-color support (256-color minimum, true-color recommended)
- Network connectivity to the MA server (WebSocket on port 8095 by default)

## macOS — Gatekeeper (unsigned binary)

The binary is not code-signed. On first launch macOS may block it. Fix with either:

- **System Settings > Privacy & Security**, scroll down, click **Open Anyway**
- One-time terminal command: `xattr -dr com.apple.quarantine xonora-cli`

Homebrew installs still require this step the first time.

## Linux — ALSA runtime

`xonora-cli` dynamically links against the ALSA runtime so it can play audio via any modern Linux distribution. Most desktops ship it pre-installed. Headless servers (or containers) may need to install it once — see [Install](Install#linux) for the package name per distro. Without ALSA, the CLI still runs as a **remote controller** (drive MA players like phones / Sonos) but cannot play local audio.

## Windows — native build

The Windows build uses **WASAPI** via miniaudio. No WSL2, no dependencies. Audio plays through whatever output device Windows is using.

WSL2 is also supported for remote-control-only use (no local audio — WSL2 doesn't expose an audio device to Linux binaries).
