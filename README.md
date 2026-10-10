# Android Media Export

[English](README.md) | [简体中文](README.zh-CN.md)

> Export photos, videos, saved images, screenshots and screen recordings from an Android phone to a computer, sorted into categories — over USB or wireless ADB.

## What this is

This is not a file copier. A file copier moves bytes and calls it done. The goal here is different: every photo accounted for, nothing duplicated, categories correct, and the whole thing re-checkable afterwards.

That distinction matters because phone-to-computer transfers fail in specific, boring ways — duplicates created by overlapping date ranges, screenshots landing in the camera folder, silent truncation when the cable is bumped. This skill is built around verifying against those failures.

## Why we open-sourced it

We built this because we were doing the same chore over and over — clearing a phone's storage before a trip, pulling an event's photos into a project folder, getting a colleague's screenshots into a shared drive. Each time, a different tool, each time a slightly different mess.

We use it in the company for exactly that: routine media offloading and archival. It is not tied to any product of ours, so it is a straightforward thing to share.

## What it does

- **Wireless ADB first.** On Android 11 and newer, wireless debugging is usually more stable than USB and often faster. No cable to knock loose, no reconnect dance.
- **Two connection modes.** Wireless ADB when available, USB as the fallback.
- **Incremental reconciliation.** Re-running the export compares against what is already on the computer instead of blindly copying again.
- **Resumable transfers.** If the connection drops mid-run, the next run continues rather than restarting.
- **Category mapping.** Photos, videos, WeChat-saved images, screenshots and screen recordings each land in their own folder, with the mapping written down rather than hard-coded by guesswork.
- **Tested across ROMs.** Xiaomi / HyperOS and stock Android behave differently in directory layout and in what the media scanner reports. Both are covered.

## Requirements

Windows · Python 3 · adb (Android Platform Tools) on PATH

## Installation

```bash
git clone https://github.com/<your-username>/android-media-export.git
```

Then place the folder into your agent skills directory:

| OS | Path |
|---|---|
| Windows | `C:\Users\<you>\.workbuddy\skills\android-media-export\` |
| macOS / Linux | `~/.workbuddy/skills/android-media-export/` |

There is no build step. Restart the session and it takes effect.

## How to use

Say what you want in plain language:

- "Copy my phone photos to the computer, sorted by category"
- "Export the phone album, it's connected over Wi-Fi"
- "Pull all phone media and split screenshots from camera shots"

The skill first establishes the connection mode, then runs the export with reconciliation, then reports counts per category so the numbers can be checked.

## Files

```
└── SKILL.md
```

## Notes and limits

1. **Wireless debugging must be enabled once.** Android requires a one-time pairing step in Developer Options before a wireless connection is possible. The repository walks through it.
2. **Category detection is heuristic.** There is no metadata field that says "this is a screenshot". The classification is built on path patterns and filename conventions, and it is documented so you can adjust it for your device.
3. **HEIC and other containers** are copied as-is. Converting them is a separate concern and is not done here.
4. **The first full export is slow.** That is the cost of verifying rather than copying.

## License

MIT
