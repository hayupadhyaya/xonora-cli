# Keybindings

Full keybinding reference for xonora-cli v0.3.10.

Keys are **case-insensitive** (`A` == `a`). Global keys work on any tab unless text input is active (in which case only `Escape` is accepted).

## Global (all tabs)

| Key       | Action |
|-----------|--------|
| `1`–`9`   | Switch to tab 1–9 |
| `Space`   | Play / Pause |
| `]`       | Next track |
| `[`       | Previous track |
| `M`       | Toggle mute (local speaker + MA server-side mute). Label is inverted: `MUTE:ON` means audio is OFF. |
| `Ctrl+R`  | Reconnect to server (refreshes all screens) |
| `?`       | Help (reserved — not yet implemented) |
| `q`       | Quit |

## Pagination (Players, Queue, Library, Logs)

| Key              | Action |
|------------------|--------|
| `Left` / `PgUp`  | Previous page |
| `Right` / `PgDn` | Next page |
| `Home`           | First page |
| `End`            | Last page |

## Tab 1 — Dashboard

Read-only. No keybindings. Panels show Now Playing, top 5 active players, and pinned players.

## Tab 2 — Players

| Key         | Action |
|-------------|--------|
| `Up` / `k`  | Move selection up |
| `Down` / `j`| Move selection down |
| `Enter`     | Select / activate player |
| `Tab`       | Open quick-select input |
| `*`         | Toggle pin on selected player |
| `+` / `=`   | Volume up |
| `-` / `_`   | Volume down |
| `P`         | Power toggle |
| `G`         | Enter group mode |
| `S`         | Toggle player selection (in group mode) |
| `U`         | Ungroup player |
| `D`         | Remove player |
| `Escape`    | Exit group mode / close input |

**Quick-select input (after `Tab`):** type a player number or name (filter is case-insensitive). `Enter` confirms, `Backspace` deletes, `Esc` cancels.

## Tab 3 — Queue

| Key          | Action |
|--------------|--------|
| `Up` / `k`   | Move selection up |
| `Down` / `j` | Move selection down |
| `Enter`      | Play selected item |
| `D`          | Delete item from queue |
| `Ctrl+Up`    | Move selected item up |
| `Ctrl+Down`  | Move selected item down |
| `C`          | Clear entire queue |
| `S`          | Toggle shuffle |
| `R`          | Cycle repeat mode |

## Tab 4 — Library

### Main list

| Key          | Action |
|--------------|--------|
| `Up` / `k`   | Move selection up |
| `Down` / `j` | Move selection down |
| `Left`       | Previous page (client-side) |
| `Right`      | Next page (client-side) |
| `>` / `.`    | Fetch next server-side batch |
| `<` / `,`    | Fetch previous server-side batch |
| `Tab`        | Next library type (albums / artists / tracks / playlists / audiobooks / podcasts / radio) |
| `Shift+Tab`  | Previous library type |
| `Enter`      | Open detail view |
| `P`          | Play selected item |
| `A`          | Add to queue |
| `F`          | Toggle favorite |
| `N`          | Create new playlist |
| `+` / `=`    | Add item to playlist |

### Detail view

| Key          | Action |
|--------------|--------|
| `Escape`     | Exit detail view |
| `Up` / `k`   | Move selection up |
| `Down` / `j` | Move selection down |
| `Enter`      | Play selected track |
| `P`          | Play entire album / playlist |
| `F`          | Toggle favorite |
| `+` / `=`    | Add track to playlist |
| `Y`          | Copy info to clipboard |

## Tab 5 — Search

| Key      | Action                          |
|----------|---------------------------------|
| `Escape` | Toggle edit / navigation mode   |
| `Enter`  | Execute search (edit mode)      |
| `Up`     | Selection up (nav mode)         |
| `Down`   | Selection down (nav mode)       |
| `P`      | Play selected result (nav mode) |

## Tab 6 — Sendspin (local audio)

| Key      | Action |
|----------|--------|
| `Up`     | Scroll up |
| `Down`   | Scroll down |
| `R`      | Reconnect (WebRTC signaling handshake) |
| `F`      | Switch to FLAC |
| `O`      | Switch to Opus |
| `P`      | Switch to PCM |
| `T`      | Run codec test |

## Tab 7 — Party

### Host view

| Key      | Action |
|----------|--------|
| `Tab`    | Switch host / guest view |
| `P`      | Start party session |
| `S`      | Skip track |
| `K`      | Kick guest |
| `X`      | End party session |

### Guest view

| Key           | Action |
|---------------|--------|
| `Tab`         | Switch host / guest view |
| `Up` / `Down` | Navigate queue |
| `G`           | Enter URL to join |
| `A`           | Add track to queue |
| `B`           | Boost queue item |
| `V`           | Vote to skip |

## Tab 8 — API Console

| Key        | Action |
|------------|--------|
| `Escape`   | Toggle edit mode |
| `Ctrl+B`   | Toggle command browser |
| `Ctrl+L`   | Clear response |
| `Enter`    | Execute command |
| `Up`       | Previous history entry |
| `Down`     | Next history entry |
| `PageUp`   | Scroll response up |
| `PageDown` | Scroll response down |
| `Tab`      | Autocomplete |

### Command browser

| Key                  | Action |
|----------------------|--------|
| `Escape`             | Exit browser |
| `Up` / `k`           | Previous command |
| `Down` / `j`         | Next command |
| `Tab` / `Right`      | Next category |
| `Shift+Tab` / `Left` | Previous category |
| `Enter`              | Select command |
| `/`                  | Start filter |
| `Backspace`          | Delete filter character |

## Tab 9 — Logs

| Key      | Action |
|----------|--------|
| `E`      | Toggle error-only filter |
| `F`      | Cycle subsystem filter |
| `X`      | Clear logs |
| `R`      | Run P-BIT (periodic built-in test) |
| `End`    | Jump to latest / enable auto-follow |
