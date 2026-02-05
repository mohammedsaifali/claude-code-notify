# claude-code-notify

Get a sound notification whenever [Claude Code](https://docs.anthropic.com/en/docs/claude-code) needs your input. Never miss when Claude is waiting on you again.

Zero dependencies. Works on Windows, macOS, and Linux.

## The Problem

You're running Claude Code, tab away to do something else, and come back 10 minutes later only to realize it's been waiting for your input the whole time.

## The Solution

A simple hook that plays a system sound every time Claude Code pauses and needs you.

## Setup

**1. Open your Claude Code settings file:**

| OS | Path |
|----|------|
| Windows | `%USERPROFILE%\.claude\settings.json` |
| macOS | `~/.claude/settings.json` |
| Linux | `~/.claude/settings.json` |

**2. Add the hook for your OS:**

### Windows

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

### macOS

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

Other macOS sound options:
- `/System/Library/Sounds/Ping.aiff`
- `/System/Library/Sounds/Pop.aiff`
- `/System/Library/Sounds/Basso.aiff`
- `/System/Library/Sounds/Hero.aiff`

### Linux

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

Alternative using `aplay`:
```json
"command": "aplay /usr/share/sounds/freedesktop/stereo/complete.oga"
```

**3. Save the file.** That's it — no restart needed.

## How It Works

Claude Code has a built-in [hooks system](https://docs.anthropic.com/en/docs/claude-code/hooks) that lets you run commands in response to events. The `Notification` event fires whenever Claude pauses and waits for user input.

- **`matcher: ""`** — matches all notifications (empty string = catch-all)
- **`type: "command"`** — runs a shell command
- **`command`** — plays a native system sound using OS built-in tools

No external packages. No audio files to download. Just your OS system sounds.

## If You Already Have Settings

If your `settings.json` already has other config, merge the `hooks` key into your existing object:

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

## Windows Sound Options

You can swap `Exclamation` for other Windows system sounds:

| Sound | Code |
|-------|------|
| Exclamation | `[System.Media.SystemSounds]::Exclamation.Play()` |
| Asterisk | `[System.Media.SystemSounds]::Asterisk.Play()` |
| Beep | `[System.Media.SystemSounds]::Beep.Play()` |
| Hand | `[System.Media.SystemSounds]::Hand.Play()` |
| Question | `[System.Media.SystemSounds]::Question.Play()` |

## License

MIT
