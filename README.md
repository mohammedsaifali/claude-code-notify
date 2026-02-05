<div align="center">

<img src="assets/banner.svg" alt="claude-code-notify" width="800" />

<br />
<br />

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20macOS%20%7C%20Linux-blue)
![Dependencies](https://img.shields.io/badge/Dependencies-Zero-brightgreen)
![Setup](https://img.shields.io/badge/Setup-30%20seconds-orange)
[![GitHub stars](https://img.shields.io/github/stars/mohammedsaifali/claude-code-notify?style=social)](https://github.com/mohammedsaifali/claude-code-notify)

</div>

---

## The Problem

You're running Claude Code, tab away to browse docs or grab coffee, and come back **10 minutes later** only to realize Claude's been sitting there waiting for you the whole time.

## The Fix

One hook. One line. Sound plays every time Claude needs you.

```
Claude working...  →  Claude pauses  →  🔔 *sound*  →  You respond
```

---

## Quick Start

**1.** Open `~/.claude/settings.json` (or `%USERPROFILE%\.claude\settings.json` on Windows)

**2.** Add the hook for your OS:

<details>
<summary><b>🪟 Windows</b></summary>

<br />

```json
{
  "hooks": {
    "Notification": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "powershell.exe -Command \"[System.Media.SystemSounds]::Exclamation.Play()\""
          }
        ]
      }
    ]
  }
}
```

**Other Windows sounds you can use:**

| Sound | Code |
|:------|:-----|
| Exclamation *(default)* | `[System.Media.SystemSounds]::Exclamation.Play()` |
| Asterisk | `[System.Media.SystemSounds]::Asterisk.Play()` |
| Beep | `[System.Media.SystemSounds]::Beep.Play()` |
| Hand | `[System.Media.SystemSounds]::Hand.Play()` |
| Question | `[System.Media.SystemSounds]::Question.Play()` |

</details>

<details>
<summary><b>🍎 macOS</b></summary>

<br />

```json
{
  "hooks": {
    "Notification": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "afplay /System/Library/Sounds/Glass.aiff"
          }
        ]
      }
    ]
  }
}
```

**Other macOS sounds you can use:**

| Sound | Path |
|:------|:-----|
| Glass *(default)* | `/System/Library/Sounds/Glass.aiff` |
| Ping | `/System/Library/Sounds/Ping.aiff` |
| Pop | `/System/Library/Sounds/Pop.aiff` |
| Basso | `/System/Library/Sounds/Basso.aiff` |
| Hero | `/System/Library/Sounds/Hero.aiff` |
| Purr | `/System/Library/Sounds/Purr.aiff` |

</details>

<details>
<summary><b>🐧 Linux</b></summary>

<br />

**PulseAudio (most distros):**

```json
{
  "hooks": {
    "Notification": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "paplay /usr/share/sounds/freedesktop/stereo/complete.oga"
          }
        ]
      }
    ]
  }
}
```

**ALSA alternative:**

```json
"command": "aplay /usr/share/sounds/freedesktop/stereo/complete.oga"
```

</details>

<br />

**3.** Save the file. **Done.** No restart needed.

---

## How It Works

```
┌──────────────────────────────────────────────────────┐
│                                                      │
│   ~/.claude/settings.json                            │
│                                                      │
│   hooks.Notification  ──→  matcher: "" (catch-all)   │
│                        ──→  plays system sound       │
│                                                      │
└──────────────────────────────────────────────────────┘
```

Claude Code has a built-in [hooks system](https://docs.anthropic.com/en/docs/claude-code/hooks) that runs commands on events. The **`Notification`** event fires whenever Claude pauses and waits for user input.

| Key | What it does |
|:----|:-------------|
| `matcher: ""` | Empty = matches **all** notifications |
| `type: "command"` | Runs a shell command |
| `command` | Plays a native OS system sound |

**Zero dependencies.** No npm packages. No audio files. Just your OS built-in sounds.

---

## Already Have Settings?

Merge the `hooks` key into your existing `settings.json`:

```json
{
  "autoUpdatesChannel": "latest",
  "hooks": {
    "Notification": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "YOUR_OS_COMMAND_HERE"
          }
        ]
      }
    ]
  }
}
```

---

## Contributing

Found a better sound command for your OS? Open a PR!

## License

[MIT](LICENSE) - Mohammed Saif Ali
