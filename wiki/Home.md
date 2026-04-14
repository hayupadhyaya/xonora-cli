# xonora-cli Wiki

Welcome to the `xonora-cli` documentation.

`xonora-cli` is a native C++ terminal client for [Music Assistant](https://music-assistant.io/). This wiki covers installation, configuration, every tab of the TUI, keybindings, the Remote (WebRTC) mode, and troubleshooting.

## Pages

- **[Getting Started](Getting-Started)** — installing, first run, auto-discovery
- **[Command-Line Flags](Command-Line-Flags)** — every flag accepted by the binary
- **[Tabs Overview](Tabs-Overview)** — what each of the 9 tabs does
- **[Keybindings](Keybindings)** — full keyboard reference
- **[Remote Mode (WebRTC)](Remote-Mode)** — connecting from outside your LAN
- **[Troubleshooting](Troubleshooting)** — known issues, logs, common fixes

## Quick reference

```sh
xonora-cli                                   # auto-discover MA server
xonora-cli --server 192.168.1.50:8095        # explicit server
xonora-cli --name "Kitchen Mac"              # set CLI's display name in MA
xonora-cli --audio                           # enable local audio on launch
xonora-cli --help                            # show all flags
```

## Project links

- Releases: <https://github.com/hayupadhyaya/xonora-cli/releases>
- Issues: <https://github.com/hayupadhyaya/xonora-cli/issues>
- Discord: <https://discord.gg/x6cWh4AjNG>
- Music Assistant: <https://music-assistant.io/>
