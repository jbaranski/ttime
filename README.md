# ttime
CLI that displays the current time in multiple formats simultaneously - local 12-hour, local 24-hour, UTC 12-hour, and UTC 24-hour. Supports an optional plus and/or minus offset. Supports accepting explicit date strings (like from various log sources).

## Why?
Remove the mental overhead of converting timestamps across different time zones when debugging issues in distributed systems with multiple log sources.

## Installing
- Put `~/.local/bin` on your system path.
- Run `make install`
- Run `ttime`

## Example usage
- Run `ttime --help`
```
[04/07/25 20:23:16] jeff@marlboro ~  > ttime --help

 Usage: ttime [OPTIONS]

╭─ Options ──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ --now                   --no-now             [default: now]                                                                                                                                            │
│ --minus                             INTEGER  [default: 0]                                                                                                                                              │
│ --plus                              INTEGER  [default: 0]                                                                                                                                              │
│ --plus-minus-uom                    TEXT     [default: days]                                                                                                                                           │
│ --date                              TEXT     [default: None]                                                                                                                                           │
│ --date-tz                           TEXT     [default: None]                                                                                                                                           │
│ --install-completion                         Install completion for the current shell.                                                                                                                 │
│ --show-completion                            Show completion for the current shell, to copy it or customize the installation.                                                                          │
│ --help                                       Show this message and exit.                                                                                                                               │
╰────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
```
- Run `ttime`
```
[04/07/25 20:23:59] jeff@marlboro ~  > ttime
Now
└── ┌─────────┬─────────────────────────────────┐
    │ local   │ 07/04/2025 08:24:00.337782-0400 │
    │         │                                 │
    │ local24 │ 07/04/2025 20:24:00.337782-0400 │
    │         │                                 │
    │ utc     │ 07/05/2025 12:24:00.337782+0000 │
    │         │                                 │
    │ utc24   │ 07/05/2025 00:24:00.337782+0000 │
    └─────────┴─────────────────────────────────┘
```
- Run `ttime --minus 4`
```
[04/07/25 20:24:14] jeff@marlboro ~  > ttime --minus 4
Now
└── ┌─────────┬─────────────────────────────────┐
    │ local   │ 07/04/2025 08:24:14.912718-0400 │
    │         │                                 │
    │ local24 │ 07/04/2025 20:24:14.912718-0400 │
    │         │                                 │
    │ utc     │ 07/05/2025 12:24:14.912718+0000 │
    │         │                                 │
    │ utc24   │ 07/05/2025 00:24:14.912718+0000 │
    └─────────┴─────────────────────────────────┘
Now - 4 days
└── ┌─────────┬─────────────────────────────────┐
    │ local   │ 06/30/2025 08:24:14.912718-0400 │
    │         │                                 │
    │ local24 │ 06/30/2025 20:24:14.912718-0400 │
    │         │                                 │
    │ utc     │ 07/01/2025 12:24:14.912718+0000 │
    │         │                                 │
    │ utc24   │ 07/01/2025 00:24:14.912718+0000 │
    └─────────┴─────────────────────────────────┘
```
- Run `ttime --plus 4 --plus-minus-uom minutes`
```
[04/07/25 20:25:14] jeff@marlboro ~  > ttime --plus 4 --plus-minus-uom minutes
Now
└── ┌─────────┬─────────────────────────────────┐
    │ local   │ 07/04/2025 08:25:15.931353-0400 │
    │         │                                 │
    │ local24 │ 07/04/2025 20:25:15.931353-0400 │
    │         │                                 │
    │ utc     │ 07/05/2025 12:25:15.931353+0000 │
    │         │                                 │
    │ utc24   │ 07/05/2025 00:25:15.931353+0000 │
    └─────────┴─────────────────────────────────┘
Now + 4 minutes
└── ┌─────────┬─────────────────────────────────┐
    │ local   │ 07/04/2025 08:29:15.931353-0400 │
    │         │                                 │
    │ local24 │ 07/04/2025 20:29:15.931353-0400 │
    │         │                                 │
    │ utc     │ 07/05/2025 12:29:15.931353+0000 │
    │         │                                 │
    │ utc24   │ 07/05/2025 00:29:15.931353+0000 │
    └─────────┴─────────────────────────────────┘
```
- Run `ttime --date "2025-07-04 14:32:17.456" --no-now`
```
[04/07/25 20:25:31] jeff@marlboro ~  > ttime --date "2025-07-04 14:32:17.456" --no-now
2025-07-04 14:32:17.456
└── ┌─────────┬─────────────────────────────────┐
    │ local   │ 07/04/2025 02:32:17.456000-0400 │
    │         │                                 │
    │ local24 │ 07/04/2025 14:32:17.456000-0400 │
    │         │                                 │
    │ utc     │ 07/04/2025 06:32:17.456000+0000 │
    │         │                                 │
    │ utc24   │ 07/04/2025 18:32:17.456000+0000 │
    └─────────┴─────────────────────────────────┘
```
- Run `ttime --date "2025-07-04T16:23:45.678+00:00" --date-tz 'US/Pacific' --no-now`
```
[04/07/25 20:43:26] jeff@marlboro ~/development/ttime main > ttime --date "2025-07-04T16:23:45.678+00:00" --date-tz 'US/Pacific' --no-now
2025-07-04T16:23:45.678+00:00
└── ┌──────────────┬─────────────────────────────────┐
    │ us/pacific   │ 07/04/2025 09:23:45.678000-0700 │
    │              │                                 │
    │ us/pacific24 │ 07/04/2025 09:23:45.678000-0700 │
    │              │                                 │
    │ utc          │ 07/04/2025 04:23:45.678000+0000 │
    │              │                                 │
    │ utc24        │ 07/04/2025 16:23:45.678000+0000 │
    └──────────────┴─────────────────────────────────┘
```
