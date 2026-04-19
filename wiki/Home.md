# xonora-cli Wiki

Welcome to the `xonora-cli` documentation.

`xonora-cli` is a native C++ terminal client for [Music Assistant](https://music-assistant.io/). This wiki covers installation, configuration, every tab of the TUI, keybindings, the Remote (WebRTC) mode, and troubleshooting.

## Pages

- **[Install](Install)** — platform-specific installation steps
- **[Downloads](Downloads)** — latest binaries and release history
- **[Supported Platforms](Supported-Platforms)** — OS/arch matrix and requirements
- **[Getting Started](Getting-Started)** — first run, configuration, what to try
- **[Command-Line Flags](Command-Line-Flags)** — every flag accepted by the binary
- **[Tabs Overview](Tabs-Overview)** — what each of the 9 tabs does
- **[Keybindings](Keybindings)** — full keyboard reference
- **[Remote Mode (WebRTC)](Remote-Mode)** — connecting from outside your LAN
- **[Troubleshooting](Troubleshooting)** — known issues, logs, common fixes

## Quick reference

```sh
# First run — pass server + credentials (saved for subsequent runs)
xonora-cli --server ws://192.168.1.50:8095 --user USERNAME --pass PASSWORD

# Subsequent runs — reuse saved config
xonora-cli
xonora-cli --name "Kitchen Mac"              # override display name
xonora-cli --audio                           # enable local audio on launch
xonora-cli --help                            # show all flags
```

## Project links

- Releases: <https://github.com/hayupadhyaya/xonora-cli/releases>
- Issues: <https://github.com/hayupadhyaya/xonora-cli/issues>
- Discord: <https://discord.gg/x6cWh4AjNG>
- Music Assistant: <https://music-assistant.io/>
