# Getting Started

## Requirements

- macOS 13 (Ventura) or later
- Apple Silicon (arm64) or Intel (x86_64) Mac
- A Music Assistant server running on your network (schema 28 or later)
- The **Sendspin** player provider enabled on the MA server
- A terminal with true-color support (Terminal.app, iTerm2, Alacritty, kitty, WezTerm)

## Install

### Homebrew

```sh
brew tap hayupadhyaya/xonora
brew install xonora-cli
```

### Manual

```sh
# Apple Silicon
curl -L -o xonora-cli.tar.gz \
  https://github.com/hayupadhyaya/xonora-cli/releases/latest/download/xonora-cli-v0.1-macos-arm64.tar.gz

# Intel
curl -L -o xonora-cli.tar.gz \
  https://github.com/hayupadhyaya/xonora-cli/releases/latest/download/xonora-cli-v0.1-macos-x86_64.tar.gz

tar -xzf xonora-cli.tar.gz
chmod +x xonora-cli
sudo mv xonora-cli /opt/homebrew/bin/          # arm64
# or: sudo mv xonora-cli /usr/local/bin/        # Intel
```

### First-launch Gatekeeper

The binary is unsigned. On first launch macOS may block it. Either:

- Open **System Settings → Privacy & Security**, scroll to the bottom, click **Open Anyway**, or
- Run once: `xattr -d com.apple.quarantine $(which xonora-cli)`

## First run

```sh
xonora-cli
```

On startup xonora-cli will:

1. Scan the local network for a Music Assistant server (mDNS `_music-assistant._tcp`)
2. Connect via WebSocket and authenticate
3. Register itself as an MA player named **"Xonora CLI"** (configurable with `--name`)
4. Connect to Sendspin, exchange hello, run clock sync
5. Open the TUI on the Dashboard tab

If no server is found, pass one explicitly:

```sh
xonora-cli --server 192.168.1.50:8095
```

## What to try first

- Press `3` to open the **Queue** tab — see what is queued on the current player
- Press `4` to open the **Library**, then `/` to search
- Press `2` to open **Players** and switch output to another MA player (Sonos, phone, etc.)
- Press `A` to enable local audio output through your Mac's speakers
- Press `Space` to play/pause
- Press `9` to see the **Logs** tab and watch MA events in real time

See [Keybindings](Keybindings) for the full reference.
