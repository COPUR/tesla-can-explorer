# Tesla CAN Explorer

Tesla CAN Explorer is an open-source research portal for browsing decoded Tesla CAN frames and signal value maps.

This research is open source on [GitHub](https://github.com/mikegapinski/tesla-can-explorer) and sponsored by [Tesla Android](https://teslaandroid.com/). Want Android apps in your Tesla? Visit [teslaandroid.com](https://teslaandroid.com/).

Independent project disclaimer: this project is unaffiliated with and not endorsed by Tesla, Inc.

## Dataset Scope

- Firmware: `2026.2`
- Sources: `libQtCarCANData.so`, `libQtCarVAPI.so`

| Source key | Vehicle / variant | Data file |
| --- | --- | --- |
| `mcu2` (default) | Model 3 MCU2 (Intel) | `./data/can_frames_decoded_all_values_mcu2.json` |
| `mcu3` | Model 3 MCU3 (AMD) | `./data/can_frames_decoded_all_values_mcu3.json` |
| `modelsx_intel` | Model S/X MCU2 (Intel) | `./data/can_frames_decoded_all_values_modelsx_intel.json` |
| `modelsx_amd` | Model S/X MCU3 (AMD) | `./data/can_frames_decoded_all_values_modelsx_amd.json` |

Related VAPI artifacts for each source key: `./data/vapi_can_digest_<key>.json` and `./data/vapi_eth_signal_aliases_<key>.csv`.

To add a data source, run `./enable_portal_source.sh --source-key <key> --label "<UI label>"` (see `--help`).

## Run Locally

```bash
python3 -m http.server 8080
```

Open:

- `http://localhost:8080/` (default: MCU2)
- `http://localhost:8080/?source=mcu3` (any source key from the table above)

Optional override:

- `http://localhost:8080/?data=./data/can_frames_decoded_all_values_mcu3.json`

## Features

- Search across frame names, addresses, signals, enum maps, enum labels, and VAPI aliases.
- Signals view: search individual signals across all frames (for example `BMS soc` or `door state`), then open one to jump to its frame with its values expanded.
- Shareable links: the URL keeps the view, search, filters, sort, selected frame and signal search.
- Export the current frame's signals (matching the signal search, all pages) as CSV, one row per decoded value.
- Keyboard navigation: `/` focuses search, arrow keys and `Home`/`End` move through the list, `Enter`/`Space` selects a frame or expands a signal.
- Independent left/right panel scrolling for easier browsing on large datasets.
- Filter by bus/module and sort by address, name, signal count, enum count, or VAPI alias count.
- Expand per-signal decoded values directly in the frame detail view.

### URL parameters

| Parameter | Meaning |
| --- | --- |
| `source` | Data source key |
| `data` | Custom JSON URL (overrides `source`) |
| `view` | `signals` for the signals view (default: frames) |
| `q` | Global search |
| `bus`, `module` | Filters, e.g. `bus=CH (5)`, `module=BMS` |
| `sort` | `name`, `signals`, `enums` or `vapi` (default: address) |
| `enum` | `1` to show only enumerated frames/signals |
| `frame` | Selected frame key (`bus\|bus_id\|address_dec\|frame_name`) |
| `sq` | Signal search within the selected frame |

## Credits

- Copyright © 2026 Michał Gapiński ([gapinski.eu](https://gapinski.eu))
- Tesla Android ([teslaandroid.com](https://teslaandroid.com/))
- X: [@mikegapinski](https://x.com/mikegapinski), [@teslaandroid](https://x.com/teslaandroid)

## License

This project is licensed under `0BSD` (see `LICENSE`).
