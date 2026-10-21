# Project - KAGOME

**Type:** AI agent → custom desktop environment built on Ubuntu

**Status:** Active - working daily driver

**Hardware:** Older HP laptop (`hexhunter@zetsu`)

---

## Objective

Build a personal system that completes real work on my own computer, not one that only talks about it.

The project went through two phases:

```text
Phase 1: The AI agent
(planning, tools, memory, autonomous tasks)
        ↓
Agent failures and bottlenecks
        ↓
Phase 2: The desktop environment
(a custom workspace built around the AI tools that actually worked)
```

The desktop environment exists because of what the agent phase taught me.

---

# Phase 1 - The AI Agent

## Goal

An agent that could plan, choose tools, run shell commands, write files, evaluate evidence, recover from errors, and remember past sessions.

## Architecture Evolution

```text
Local agent
(offline, private, custom Python + Ollama)
        ↓
Network-first agent
(cloud reasoning by default, offline for basic tasks only)
        ↓
OpenHands Agent SDK
(established framework, legacy agent kept as fallback)
```

| Component | What it does |
|-----------|--------------|
| `memory.sqlite3` | Persistent memory database |
| Session module | Keeps completed exchanges, archives older ones as unverified history, and manages context size |
| REA MCP server | Reverse-engineering tools integrated into the agent |
| OpenAI Codex CLI | Engineering agent used to write and modify the agent's code |

## What Worked

- File-writing and shell-execution tests succeeded.
- Persistent memory and session continuity worked.
- A continuity test recalled a test marker from earlier in the session (1,246 cached tokens, 4,096-token context with 768 reserved).

## What Did Not Work

- Reliable independent completion of complex tasks was never established.
- A reverse-engineering challenge on `/usr/bin/sha256sum` remained unverified.
- 42 regression test cases were reported passing, but independent completion of complex tasks was never established.

---

# Bottlenecks and How I Got Past Them

| Bottleneck | What I saw | What I did |
|------------|------------|------------|
| Hardware | An offline terminal response took **198 seconds** | Switched to network-first: cloud reasoning by default, offline only for basic tasks |
| Building everything from scratch | Rebuilding systems that already exist | Chose to reuse established open-source tools: OpenHands, Hyprland, Waybar, mpv |
| Context limits | A 4,096-token context limit | Built a session module to archive older exchanges and manage context size |
| Incremental fixes | Many small patches without the real goal getting closer | Stopped judging progress by reports and judged it by real task completion |
| Cost | No paid model API key | Looked for free options, then used Claude Code as my main agent instead of forcing my own agent to do everything |
| Outdated packages | Ubuntu's `yt-dlp` was 7 months old and YouTube rejected it | Installed current official releases, verified with SHA256 checksums |

---

# Correcting My AI Tools

Working with AI agents taught me that their reports are claims, not evidence.

I had to step in and correct them several times:

### "The tests pass" ≠ "It works"

Codex reported milestones and passing regression tests, but the agent still could not reliably finish complex tasks on its own.

I rejected test results as proof of progress and made **real-world task completion** the only measure that counts.

---

### Offline-first was the wrong direction

Earlier guidance pushed the agent toward running fully offline.

The 198-second response showed this hardware could not support it, so I corrected the direction to network-first.

---

### A passing test on the wrong thing

While building the video window, a test reported that `yt-dlp` could get a playable stream, so YouTube seemed fine.

Actual playback still failed with `HTTP 403`. Only testing the real action exposed the problem.

---

### Instructions that could not work

I was told to run `sudo` through Claude Code's `!` prompt.

It failed because `sudo` needs a real terminal to ask for a password, and that prompt has none. I ran it in a normal terminal instead.

---

### Holding the agent to my rules

I required the agent to check existing shortcuts before adding new ones. It found that Super+P, which I had asked for, was already used for pseudo-tiling, so I picked Super+O instead of overwriting it.

I also set rules that agents had to follow every time:

- Never claim a command succeeded without verifying the result.
- Back up every file before changing it.
- Don't treat old statements or guesses as confirmed facts.

---

# Phase 2 - The Desktop Environment

## Why It Changed

The agent could not reliably do complex work alone, but AI coding agents working **with me** could.

So instead of forcing an autonomous agent, I built a workspace around the tools that actually worked: the terminal, Claude Code, live system monitoring, and fast keyboard control.

## Requirements I Set Before Building

- Runs as its own session, selectable from the login screen.
- The normal Ubuntu session stays untouched as a fallback.
- Modular, so features can be added without rebuilding everything.
- Inspect the hardware, graphics, and display before choosing a compositor or changing anything.
- Every shortcut is **Super + one key**. No Shift or Ctrl combinations, and no key doing two jobs.

## Architecture

```text
Login screen
     ↓
KAGOME session (Hyprland compositor)
     ↓
┌─────────────┬──────────────┬──────────────┬──────────────┐
│ Waybar      │ Command      │ foot         │ The Screen   │
│ top bar     │ centre       │ terminal     │ mpv window   │
│ live stats  │ (Super+D)    │ (Super+Enter)│ (Super+Y)    │
└─────────────┴──────────────┴──────────────┴──────────────┘
     ↓
One palette file in theme/ that every component reads from
```

| Component | What it does |
|-----------|--------------|
| Hyprland | Wayland compositor. Draws windows, borders, animations, and handles every keybind. |
| Waybar | Top bar with workspaces, clock, CPU, RAM, temperature, network, volume, and battery. |
| Command centre | GTK4 layer-shell panel with live gauges, an event log, a process killer, and quick actions. |
| foot | Terminal, with a floating zoom-in mode and a slide-down console (Super+`). |
| Feedback daemon | Background process that confirms actions with pop-ups (copy/paste, volume, Wi-Fi, battery warnings). |
| The Screen | Small floating window that loops animations or plays YouTube on demand. |
| Theme system | One palette file in `theme/` that components read from. A script generates the terminal's colours from it. |

Everything lives in `~/.config/kagome/`. Every change starts with a backup of the files being edited.

---

## Problems Solved

### Problem 1 - Alt+Tab Could Not Raise Floating Windows

**Symptom:** Alt+Tab switched windows, but some windows stayed hidden behind others.

**Investigation:** Chrome was stuck in a tiled/scratchpad state while other windows floated. Tiled and floating windows sit on different layers.

**Fix:** Corrected the window state so Alt+Tab raises the selected window.

---

### Problem 2 - Browser Cut Off by the Top Bar

**Symptom:** Chrome's tab strip was hidden behind Waybar.

**Investigation:** Every window floats. Floating windows ignore the space reserved for the bar. Chrome reopened at its saved position (`9,9`, `1582×882`), so the bar covered the tabs.

**Root cause:** Reserved space only applies to tiled windows.

**Fix:** A window rule opens browsers inside the usable area (`8,42`, `1584×850`).

---

### Problem 3 - YouTube Rejected the Stream (HTTP 403)

**Symptom:** A test reported a playable stream, but actual playback failed with `HTTP 403`.

**Investigation:**

- Ubuntu's packaged `yt-dlp` was about 7 months old.
- YouTube changes its checks every few weeks, and current versions need a JavaScript runtime.

**Options considered:**

1. Upstream `yt-dlp` + `deno` in `~/.local/bin` (chosen)
2. Ubuntu's `nodejs` with the old `yt-dlp`
3. Leave YouTube for later

**Fix:** Installed the current official releases of `yt-dlp` and `deno`, **after verifying each download against its published SHA256 checksum**.

A checksum is a fingerprint of the file. If it matches what the developer published, the file was not tampered with.

---

### Design Decision - Full Paths Instead of PATH

**Situation:** The new `yt-dlp` and `deno` were installed in `~/.local/bin`, but the KAGOME session's `PATH` does not include that folder.

**Risk:** Without a fix, the Screen could use the old `yt-dlp`, or fail to find the new tools at all.

**Decision:** The Screen passes both tools to `mpv` by full path, so it never depends on `PATH`.

---

### Problem 4 - Terminal Ignored the Theme

**Symptom:** After the retheme, the terminal kept its old colours.

**Root cause:** `foot.ini` had no colour settings at all, so foot used its built-in defaults. The prompt and login banner were set separately in `~/.bashrc`.

**Fix:** The theme script now generates foot's colours from the palette, and the prompt and banner read the same palette.

---

### Problem 5 - Unwanted Notifications

**Symptom:** Every Super+Y would have triggered a "Moved to workspace" pop-up.

**Root cause:** The feedback daemon reports window moves, and hiding the Screen moves it to a hidden workspace.

**Fix:** The Screen records its window address, and the daemon skips that window.

---

## The Screen - Design Decisions

- **Pre-rendered animations:** five seamless loops (sigil ring, ink smoke, red static, falling ash, candle) rendered once with Python and `ffmpeg`, then looped by `mpv`.
- **Hard content rule:** no text, numbers, or glyphs in any animation. Frames were checked after rendering.
- **Muted by default:** every video starts muted. Unmuting only lasts for one video.
- **No polling:** the controller waits on mpv's IPC events and Unix signals instead of checking in a loop.
- **Self-healing:** a failed link shows a pop-up and returns to the animations. If `mpv` crashes, it restarts.
- **Measured cost:** about 8% of one CPU core while visible, zero while hidden.

---

## Tools Used

| Area | Tools |
|------|-------|
| AI assistance | ChatGPT (guidance), OpenAI Codex CLI, Claude Code |
| Agent | Python, Ollama, OpenHands Agent SDK, SQLite, REA MCP (Ghidra) |
| Desktop | Hyprland, Waybar, GTK4 layer-shell, foot, fuzzel, mako, hyprlock, hyprpaper |
| Media | mpv, yt-dlp, deno, ffmpeg, NumPy |
| Verification | SHA256 checksums, `hyprctl`, config backups |

---

## Commands Used

```bash
# Reload Hyprland after config changes
hyprctl reload

# Install the Screen's dependencies
sudo apt install --no-install-recommends mpv yt-dlp ffmpeg python3-numpy

# Update yt-dlp when YouTube breaks it
~/.local/bin/yt-dlp -U

# Take a delayed screenshot of the desktop
sleep 3 && grim ~/Pictures/kagome.png
```

---

## Lessons Learned

- Measure real-world results, not milestones or self-graded tests.
- AI reports are claims. Verify them like any other evidence.
- A test that passes on the wrong thing proves nothing.
- Hardware limits decide architecture.
- Reuse established tools before building custom ones.
- Keep a fallback. Experiments should never be able to lock me out.
- Back up every file before changing it.
- One palette file is easier than ten.
- Floating windows do not respect reserved space.
- Verify downloads with checksums before running them.
- Never assume `PATH`. Use full paths for anything critical.
- `sudo` needs a terminal. Background shells cannot ask for passwords.
- If something "ignores" a setting, check whether the setting exists at all.

---

## Next Steps

- Investigate Wi-Fi card driver crashes seen in the event log.
- Fix the close-window animation, which is not visibly showing.

---

## Final Status

**KAGOME: Working daily driver**

The agent phase showed what didn't work. The desktop phase turned those lessons into a system I use every day.
