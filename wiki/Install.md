# Install

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

## Verify installation

```sh
xonora-cli --version
xonora-cli --help
```

## Gatekeeper (macOS, unsigned binary)

The binary is not code-signed. On first launch macOS may block it. Fix with either:

- **System Settings > Privacy & Security**, scroll down, click **Open Anyway**
- One-time terminal command: `xattr -dr com.apple.quarantine $(which xonora-cli)`

Homebrew installs still require this step the first time.

## Next steps

See [Getting Started](Getting-Started) for first-run configuration.
