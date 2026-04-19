# Getting Started

## Requirements

- macOS 12 (Monterey) or later (Apple Silicon — Intel: build from source), Linux (glibc 2.28+), or Windows 10+ (see [Supported Platforms](Supported-Platforms) for full matrix)
- A Music Assistant server running on your network (schema 28 or later)
- The **Sendspin** player provider enabled on the MA server
- A terminal with true-color support (Terminal.app, iTerm2, Alacritty, kitty, WezTerm, Windows Terminal)

## Install

### Homebrew (macOS arm64 + Linux)

```sh
brew install hayupadhyaya/xonora/xonora-cli
```

See [Install](Install) for manual downloads on all platforms (macOS, Linux, Windows).

### First-launch Gatekeeper (macOS)

The binary is unsigned. On first launch macOS may block it. Either:

- Open **System Settings > Privacy & Security**, scroll to the bottom, click **Open Anyway**, or
- Run once: `xattr -dr com.apple.quarantine $(which xonora-cli)`

## First run

Initial setup requires passing your server URL and credentials:

```sh
xonora-cli --server ws://192.168.1.50:8095 --user myuser --pass mypass
```

Or with a token:

```sh
xonora-cli --server ws://192.168.1.50:8095 --token YOUR_TOKEN
```

On first successful connection, the settings are saved to `config.json` in the platform config directory:

- **macOS:** `~/Library/Application Support/xonora/config.json`
- **Linux:** `$XDG_CONFIG_HOME/xonora/config.json` (or `~/.config/xonora/config.json`)
- **Windows:** `%APPDATA%\xonora\config.json`

Subsequent runs can simply be:

```sh
xonora-cli
```

On startup xonora-cli will:

1. Connect via WebSocket and authenticate against the saved MA server
2. Register itself as an MA player named **"Xonora CLI"** (configurable with `--name`)
3. Connect to Sendspin, exchange hello, and run clock synchronization
4. Open the TUI on the Dashboard tab

## What to try first

- Press `3` to open the **Queue** tab — see what is queued on the current player
- Press `4` to open the **Library**, then `/` to search
- Press `2` to open **Players** and switch output to another MA player (Sonos, phone, etc.)
- Press `Space` to play/pause
- Press `M` to toggle mute (label `MUTE:ON` means audio is OFF)
- Launch with `--audio` to enable local audio on startup
- Press `9` to see the **Logs** tab and watch MA events in real time

See [Keybindings](Keybindings) for the full reference.
