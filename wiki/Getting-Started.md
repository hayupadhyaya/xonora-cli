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

Initial setup requires passing your server URL and credentials:

```sh
xonora-cli --server ws://192.168.1.50:8095 --user myuser --pass mypass
```

Or with a token:

```sh
xonora-cli --server ws://192.168.1.50:8095 --token YOUR_TOKEN
```

On first successful connection, the settings are saved to `~/.xonora-cli/config.json`. Subsequent runs can simply be:

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
- Press `A` to enable local audio output through your Mac's speakers
- Press `Space` to play/pause
- Press `9` to see the **Logs** tab and watch MA events in real time

See [Keybindings](Keybindings) for the full reference.
