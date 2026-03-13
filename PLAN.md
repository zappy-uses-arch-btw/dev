# BlinkWM - Complete Project Plan

---

## 1. Project Overview

**BlinkWM** - A minimal, fast, macOS/Deepin-inspired hybrid tiling window manager for X11 written in Rust.

### Design Goals
- Blazing fast (<2s startup, <30MB RAM)
- Potato PC friendly
- Minimal + Clean + Modern macOS/Deepin design
- Native X11 implementation (no external bars)
- No bloat - essential features only

### Version Requirements
- Use **latest stable** versions of all dependencies
- Rust: stable channel (run `rustup update stable`)
- All crates: latest version from crates.io
- All system packages: latest from official repos/AUR

---

## 2. TUI Layouts

### blink-launch (App Launcher)
- **Style**: Spotlight popup
- **Size**: 600x400px (centered)
- **Position**: Center of screen

```
┌─────────────────────────────────────────────────────────────┐
│  > Search apps...                               ⌘  ✕       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Type to search...                                          │
│                                                             │
└─────────────────────────────────────────────────────────────┘

[After typing]:
┌─────────────────────────────────────────────────────────────┐
│  > term                                          ⌘  ✕       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Alacritty                     󰜝 Run in terminal          │
│  Kitty                         󰀮 Add to favorites         │
│  Terminal                      󌋢 App info                 │
│  URxvt                                                 │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### blink-conf (Config Tool)
- **Style**: macOS Spotlight-style compact TUI
- **Size**: 700x500px (centered)
- **Position**: Center of screen

```
┌─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│  󰘘 blink-conf                               > Search settings...    ⌘   [Save] [Apply] [Reset] [Profiles] [Export] │
├─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                                                             │
│  󰒖 System Settings                                                                                                         │
│  󰌵 Keybindings                                                                                                             │
│  󰈞 Theming                                                                                                                 │
│  󰘚 Window Rules                                                                                                            │
│  󰑹 Workspaces                                                                                                              │
│  󰡒 Layout Settings                                                                                                         │
│  󰡜 Bar Configuration                                                                                                       │
│  󰐞 Autostart Apps                                                                                                          │
│  󰾆 Picom Settings                                                                                                          │
│  󰍜 Wallpaper                                                                                                               │
│  󰡱 Profiles                                                                                                                │
│  󰡜 Advanced Settings                                                                                                       │
│  󰡜 Export/Import                                                                                                           │
│  󰡜 Help                                                                                                                    │
│                                                                                                                             │
│  ┌───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐  │
│  │  Live Preview:                                                                                                          │  │
│  │  [1] [2] [3] │ Firefox - BlinkWM │ 󰘚 12% │ 󰈐 45% │ 󰰯 Wed Mar 11 10:30                                            │  │
│  │                                                                                                                         │  │
│  │  [Alacritty] [Firefox] [VS Code] [Discord]                                                                        │  │
│  │  ┌─────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐  │  │
│  │  │  Workspace 1: BSP Layout                                                                                            │  │  │
│  │  │  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐                                                                │  │  │
│  │  │  │   Firefox   │ │  Terminal   │ │   Code      │                                                                │  │  │
│  │  │  │             │ │             │ │             │                                                                │  │  │
│  │  │  │             │ │             │ │             │                                                                │  │  │
│  │  │  └─────────────┘ └─────────────┘ └─────────────┘                                                                │  │  │
│  │  └─────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘  │  │
│  └───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘  │
│                                                                                                                             │
│  System Info: OS: Arch Linux x86_64 | CPU: Ryzen 7 5800X | RAM: 32GB | GPU: RTX 3080 | Monitor: 1920x1080 @ 144Hz          │
│                                                                                                                             │
└─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
```

**Compact Config Tool Features:**
- **macOS Spotlight Style**: Clean, centered popup design
- **Search-Driven**: Filter settings with search bar
- **Live Preview**: Real-time workspace visualization
- **System Info**: Compact system monitoring at bottom
- **Essential Sections**: Focused on core configuration options
- **Quick Actions**: Save, Apply, Reset, Profiles, Export buttons
- **Minimal Footprint**: Takes only 700x500px space

### Power Menu (Goodbye, $USER)
- **Style**: Single row macOS-style menu
- **Size**: 800x120px (centered)
- **Position**: Center of screen
- **Title**: "Goodbye, [username]" (e.g., "Goodbye, bhishma")

```
┌─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│  Goodbye, bhishma                                                                                                           │
├─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                                                             │
│  [󰐥 Lock]   [󰤄 Sleep]   [󰍃 Hibernate]   [󰤂 Reboot]   [󰐦 Power Off]   [󰍃 Suspend]   [󰍃 Logout]   [󰙯 Switch User]   [✕ Cancel] │
│                                                                                                                             │
└─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
```

### blink Utility Menu (Compact System Tray Style)
- **Style**: Windows system tray compact popup with categorized settings
- **Size**: 320x450px (right-aligned, near system tray)
- **Position**: Right side of screen, anchored to system tray area

```
┌─────────────────────────────────────────────────────────────┐
│  咪 Volume: ████████████░░░░░░░  65%    󰼡 Brightness   │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  󰘚 Window Management                                        │
│  󰤨 Move Window                                            │
│  󰺀 Resize Window                                          │
│  󰡭 Close Window                                           │
│  󰑔 Focus Window                                           │
│  󰋡 Raise/Lower                                            │
│                                                             │
│  󰑹 Workspace & Layout                                     │
│  󰡒 Switch Workspace                                       │
│  󰡜 BSP Layout                                             │
│  󰡜 Grid Layout                                            │
│  󰡜 Monocle Layout                                         │
│  󰡜 Spiral Layout                                          │
│                                                             │
│  󰑔 System Tools                                           │
│  󰋡 Screenshot                                             │
│  󰾔 Media Controls                                         │
│  󰈔 CPU/Memory                                             │
│  󰽢 Notifications                                          │
│  󰙅 Lock Screen                                            │
│                                                             │
│  󰡱 Settings                                               │
│  󰡱 Config Tool                                            │
│  󰡱 Package Manager                                        │
│  󰡱 Display Settings                                       │
│  󰡱 Network Settings                                       │
│  󰡱 Sound Settings                                         │
│                                                             │
│  󰡱 Quick Actions                                          │
│  󰡱 Help                                                   │
│  󰡱 About                                                  │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

**Compact Utility Menu Features:**
- **System Tray Style**: Compact, right-aligned popup like Windows system tray
- **Live Controls**: Volume and brightness sliders at top
- **Categorized Settings**: Organized into 5 clear categories:
  - **Window Management**: Complete window operations
  - **Workspace & Layout**: Workspace and layout management
  - **System Tools**: Essential system utilities
  - **Settings**: Configuration and system settings
  - **Quick Actions**: Help and information
- **Quick Access**: Essential tools accessible with single clicks
- **Minimal Footprint**: Takes minimal screen space while providing full functionality
- **Contextual**: Appears near system tray for familiar user experience

### Minimal Status Bar (Default)
- **Position**: Top
- **Height**: 24px

```
┌─────────────────────────────────────────────────────────────────────┐
│ [1] [2] [3] │ Firefox - BlinkWM │ 󰘚 12% │ 󰈐 45% │ 󰰯 Wed Mar 11 10:30 │
└─────────────────────────────────────────────────────────────────────┘
  ↑                              ↑                        ↑                   ↑
  Workspaces                    Center title             System stats        Clock
```

### Full Status Bar (Optional)
- **Position**: Top
- **Height**: 24px

```
┌─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│ [1] [2] [3] │ BSP │ 󰒖 Firefox │ 󰤨 WiFi │ 󰕫 85% │ 咪 65% │ 󰼡 80% │ 󰈔 55°C │ 󰽢 │ 󰕫 │ 󰰯 Wed Mar 11 10:30 │ ✉ │
└─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
  ↑        ↑      ↑       ↑         ↑        ↑       ↑        ↑      ↑    ↑    ↑         ↑          ↑
Workspaces Layout Title   WiFi    Battery   Volume  Brightness Temp   Media Notif Clock      Tray
```

---

## 3. Architecture

### Simplified Architecture (No Bloat)
```
BlinkWM/
├── blink-wm/           # Core window manager + native X11 bar (Rust)
├── blink-launch/      # App launcher TUI
├── blink-conf/        # Config TUI
├── blink/             # Essential utility CLI tool
└── blink-ipc/         # Shared IPC library
```

### Native X11 Bar Implementation
- **Integrated**: Bar is built into `blink-wm` core (no separate process)
- **Native X11**: Uses X11 drawing primitives (like dwm)
- **Performance**: Zero overhead, no IPC latency
- **macOS Style**: Top position, 24px height, clean design

### Tech Stack
| Component | Technology |
|-----------|------------|
| WM Core + Bar | Rust + x11rb (native X11) |
| Keyboard | xkbcommon |
| Config | Lua (mlua) |
| TUI Framework | Ratatui + Crossterm |
| IPC | Unix socket (i3-compatible) |

---

## 4. Core Window Manager (blink-wm)

### Features
| Feature | Description |
|---------|-------------|
| **Hybrid Tiling** | Tiling + Floating modes |
| **Layouts** | BSP, Grid, Main+Stack, Monocle, Spiral |
| **Workspaces** | Dynamic, multi-monitor support |
| **Scratchpad** | Hide/show windows with shortcut |
| **Smart Borders** | Hide when single window |
| **Smart Gaps** | No gaps when single window |
| **Marked Windows** | Mark for batch operations |
| **Window Rules** | Per-app float/size/position/opacity |
| **Per-workspace Layout** | Different layout per workspace |
| **Auto-floating** | Auto-float dialogs |
| **Global Fullscreen** | Fullscreen across monitors |
| **Focus Mode** | Click to focus + sloppy focus |
| **Autostart** | Execute `~/.config/blink-wm/autostart.sh` on launch |
| **Live Reload** | Reload config via IPC without restart (`blink reload`) |

### Startup Sequence
On launch, `blink-wm` will:
1. Connect to X11 display
2. Parse `~/.config/blink-wm/config.lua` (fall back to defaults on error)
3. Apply colorscheme from `~/.config/blink-wm/colors.ini`
4. Initialize native X11 status bar
5. Execute `~/.config/blink-wm/autostart.sh` if it exists
6. Begin the X11 event loop

### Standards
- EWMH/ICCCM compliance
- X11 session management

---

## 5. Status Bar (blink-bar)

### Default (Minimal)
| Position | Content |
|----------|---------|
| Left | Workspaces (occupied only) |
| Center | Focused window title |
| Right | CPU % \| RAM % \| Date/Time |

### Full Bar (Optional)
- Workspaces, Layout indicator, App launcher
- WiFi, Battery, Volume, Brightness
- CPU temp, Media player, Notifications
- System tray, Clock

### Architecture
**Native X11 Bar**: The status bar is built directly into `blink-wm` core using native X11 drawing primitives (like dwm). No separate process, no IPC overhead.

### Features
- **Native X11**: Direct X11 drawing (no external dependencies)
- **macOS Style**: Top position, 24px height, clean design
- **Zero Overhead**: No IPC latency, integrated with WM core
- **Theme Adaptive**: Colors follow system theme
- **Minimal**: Only essential modules (workspaces, title, system stats, clock)

---

## 6. App Launcher (blink-launch)

### Design
- Spotlight-style popup (600x400px, centered)
- No icons - text only
- `>` prefix in search bar
- Lazy loading - no preloading
- Blazing fast fuzzy search

### Features
- Search apps on type
- Recent apps at top
- Right-click context menu:
  - Run
  - Run in Terminal
  - Run as Root
  - Add to Favorites

---

## 7. Config Tool (blink-conf)

### Interface
- macOS Spotlight-style TUI (700x500px, centered)
- Search-driven navigation with filterable settings
- Live preview panel with real-time workspace visualization
- Compact system monitoring at bottom
- Essential configuration sections only

### Sections
| Section | Features |
|---------|----------|
| **System Settings** | Live system monitoring, performance metrics, hardware info |
| **Keybindings** | Visual editor, key recorder, conflict detection |
| **Theming** | Colors, transparency, font control, live preview |
| **Window Rules** | Window rules, floating rules, size/position presets |
| **Workspaces** | Count, names, monitors, per-workspace settings |
| **Layout Settings** | Gaps, borders, padding, layout-specific settings |
| **Bar Configuration** | Modules, order, visibility, custom modules |
| **Autostart Apps** | Startup apps, startup scripts |
| **Picom Settings** | Backend selection, blur settings, animations |
| **Wallpaper** | Set wallpaper, generators, slideshow |
| **Profiles** | Gaming, Productivity, Battery, Custom with one-click switching |
| **Advanced Settings** | Debug settings, performance tuning, X11 options |
| **Export/Import** | Config backup, sharing, version control integration |
| **Help** | Documentation, troubleshooting, community resources |

### Live Reload
Config changes made in `blink-conf` are applied **immediately** via IPC — no restart required. The [Apply] button sends a `blink reload` IPC message to `blink-wm`. Colorscheme changes also hot-reload without restarting the bar or compositor.

### Colorscheme Format (Key=Value Tags)
```ini
Borders=#3c3c3c
BordersActive=#007ACC
Background=#1e1e1e
Surface=#252526
Text=#cccccc
Accent=#007ACC
```

> **Tip:** Colorschemes from `pywal`, `wallust`, and `hellwal` can be imported — their JSON output is automatically converted to this Key=Value format.

---

## 8. Utility Tool (blink)

### Compact Menu (600x450px)
- Volume slider + brightness slider at top
- 3-column icon grid
- Opens config TUI via Settings

### Commands
| Category | Commands |
|----------|----------|
| **Window** | list, move, resize, close, focus, raise, lower |
| **Output** | list, enable, disable, primary, mode |
| **Workspace** | switch, move, create, delete, rename |
| **Layout** | list, set, next, prev |
| **Screenshot** | full, region, window, clipboard |
| **Clipboard** | copy, paste, history, clear |
| **Media** | vol, bright, play, pause, next, prev |
| **System** | cpu, mem, battery, disk |
| **Session** | lock, sleep, reboot, poweroff, logout |

---

## 9. Package Installer (blink-pkg)

### Design
- Custom Nala-like TUI (clean, beautiful UI)
- Compact popup (600x450px, centered)
- `>` prefix in search bar

### Features
- Fuzzy search packages
- Multi-select install with checkboxes
- Install/Remove/Update with progress bars
- Show package details (deps, size, repo)
- Clean color output

### UI Layout
```
┌─────────────────────────────────────────────────────────────┐
│  > Search packages...                            ⌘    ✕    │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  □ alacritty  terminal emulator              [core]   1.2MB │
│  □ firefox    web browser                  [extra]  150MB  │
│  □ vscode    code editor                   [AUR]   200MB   │
│  □ discord   chat app                      [AUR]   120MB   │
│                                                             │
│  [Install] [Remove] [Update] [Info]                        │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Backend
- Uses pacman for official repos
- Uses yay/paru for AUR

---

## 10. Performance

| Metric | Target |
|--------|--------|
| Startup | <2 seconds |
| Memory | <50MB (WM core) |
| CPU Usage | Near zero idle |

### Optimizations
- Event-driven UI (no polling)
- Throttled updates (CPU/RAM: 5-10s, Clock: 1min)
- Lazy loading (app launcher)
- Async Rust (Tokio)
- Minimal dependencies (pure Rust)
- Smart caching

---

## 11. Dependencies

### Required (Arch Linux)
- **Rust** (official: `rust`)
- **x11rb** (crate - not a system package)
- **xkbcommon** (official: `libxkbcommon`)
- **mlua** (crate - not a system package, features = ["lua54", "vendored"])
- **ratatui** + **crossterm** (crates - not system packages)
- **JetBrains Mono** (official: `ttf-jetbrains-mono`)
- **Nerd Fonts** (AUR: `ttf-jetbrains-mono-nerd` or `nerd-fonts-complete`)

### Optional (Arch Linux)
- **hellwal** (AUR)
- **wallust** (AUR)
- **pywal** (official: `python-pywal`)
- **picom-git** (AUR - recommended for blur/animation)

---

## 12. Todo List

### Phase 1: Core Window Manager
- [ ] Set up project structure (Cargo workspace with all crates)
- [ ] Define and document IPC message types and wire format (blink-ipc)
- [ ] Implement X11 connection and event loop in blink-wm core
- [ ] Implement window management (detect, reparent, manage windows)
- [ ] Implement tiling layouts in order: Monocle → Main+Stack → Grid → BSP → Spiral
- [ ] Implement workspace management (dynamic, multi-monitor via RandR)
- [ ] Implement keybinding system with xkbcommon
- [ ] Implement floating mode and window rules
- [ ] Implement scratchpad feature
- [ ] Implement smart borders and smart gaps
- [ ] Implement EWMH/ICCCM compliance
- [ ] Implement IPC socket server (i3-compatible wire format)
- [ ] Implement live config reload via IPC (`blink reload`)
- [ ] Implement Lua config parsing (mlua, expose blink.keys / blink.rules / blink.theme)
- [ ] Implement colorscheme system with Key=Value format
- [ ] Implement panic handler for graceful X11 cleanup on crash

### Phase 2: Status Bar
- [ ] Build blink-bar status bar (minimal default)
- [ ] Add bar modules (CPU, RAM, workspaces, title)
- [ ] Add full bar modules (optional)

### Phase 3: App Launcher
- [ ] Build blink-launch app launcher TUI
- [ ] Implement fuzzy search with lazy loading
- [ ] Add context menu for launcher

### Phase 4: Config Tool
- [ ] Build blink-conf config TUI
- [ ] Implement theming section with font control
- [ ] Implement profile system (Gaming, Productivity, Battery)

### Phase 5: Utility Tool (Essential Only)
- [ ] Build blink utility CLI tool
- [ ] Implement window operations (list, move, resize, close)
- [ ] Implement screenshot functionality
- [ ] Implement clipboard manager
- [ ] Implement media controls (volume, brightness, player)
- [ ] Implement system info (CPU, RAM, battery)
- [ ] Implement session controls (lock, sleep, reboot, poweroff)

### Phase 6: Utility Menu
- [ ] Build compact utility menu TUI
- [ ] Add volume/brightness sliders to utility menu

### Phase 7: Integrations
- [ ] Integrate picom configuration in blink-conf
- [ ] Add wallpaper/color generator integration (hellwal, wallust, pywal)
- [ ] Implement X session management
- [ ] Add display manager integration

### Phase 8: Optimization & Polish
- [ ] Performance optimization (event-driven, throttled updates)
- [ ] Create default config files and colorschemes
- [ ] Test and polish all components

---

## 13. Arch Linux Packaging

### PKGBUILD Structure
```
blink-wm/
├── PKGBUILD
├── .SRCINFO
└── files/
    ├── blink-wm.service
    ├── blink.desktop
    └── blink-wm.sh
```

### Package Contents
```
usr/bin/blink-wm         # Main executable
usr/bin/blink            # Utility CLI
usr/bin/blink-launch     # App launcher
usr/bin/blink-conf       # Config tool
usr/bin/blink-bar        # Status bar
usr/bin/blink-pkg        # Package installer
usr/lib/systemd/system/blink-wm.service  # Systemd service
usr/share/xsessions/blink.desktop       # LightDM/SDDM
usr/share/blink-wm/      # Config directory
```

### Dependencies (Arch Linux)
- rust
- libxkbcommon
- ttf-jetbrains-mono
- ttf-jetbrains-mono-nerd (AUR)

### Optional
- picom-git (AUR)
- hellwal (AUR)
- wallust (AUR)
- python-pywal (official)

---

## 14. Default Keybindings

**Modifier key:** `Super` (Mod4 / Windows key)

### Essential
| Keybinding | Action |
|------------|--------|
| `Super + Return` | Launch terminal |
| `Super + Space` | Open app launcher (blink-launch) |
| `Super + Q` | Close focused window |
| `Super + F` | Toggle fullscreen |
| `Super + T` | Toggle floating mode |
| `Super + M` | Toggle monocle layout |
| `Super + B` | Toggle status bar visibility |
| `Super + Shift + R` | Reload config (`blink reload`) |
| `Super + Shift + Q` | Quit blink-wm |

### Focus & Movement
| Keybinding | Action |
|------------|--------|
| `Super + H/J/K/L` | Focus left/down/up/right |
| `Super + Shift + H/J/K/L` | Move window left/down/up/right |
| `Super + Ctrl + H/L` | Resize window (shrink/grow) |
| `Super + Tab` | Cycle focus forward |
| `Super + Shift + Tab` | Cycle focus backward |

### Workspaces
| Keybinding | Action |
|------------|--------|
| `Super + 1-9` | Switch to workspace 1-9 |
| `Super + Shift + 1-9` | Move window to workspace 1-9 |
| `Super + Ctrl + Right/Left` | Next/previous workspace |

### Layouts
| Keybinding | Action |
|------------|--------|
| `Super + E` | BSP layout |
| `Super + G` | Grid layout |
| `Super + S` | Main+Stack layout |
| `Super + Shift + M` | Monocle layout |
| `Super + Shift + S` | Spiral layout |

### Utilities
| Keybinding | Action |
|------------|--------|
| `Super + P` | Open utility menu (blink) |
| `Super + Shift + P` | Open package installer (blink-pkg) |
| `Super + Shift + C` | Open config tool (blink-conf) |
| `Super + Grave` | Toggle scratchpad |
| `Print` | Screenshot (full screen) |
| `Super + Print` | Screenshot (region select) |
| `Super + V` | Open clipboard history |

---

## 15. Lua Config API

The config file lives at `~/.config/blink-wm/config.lua`. On parse error, `blink-wm` falls back to built-in defaults and logs the error — it never crashes.

```lua
-- ~/.config/blink-wm/config.lua

local blink = require("blink")

-- General settings
blink.config = {
    mod          = "Super",          -- Modifier key
    terminal     = "alacritty",      -- Default terminal
    launcher     = "blink-launch",   -- App launcher command
    border_width = 2,                -- px
    gap_size     = 8,                -- px (inner + outer)
    focus_follow = false,            -- Sloppy focus
    smart_gaps   = true,             -- No gaps with single window
    smart_borders = true,            -- No borders with single window
}

-- Keybindings
blink.keys = {
    { mod = {"Super"},         key = "Return", action = blink.spawn(blink.config.terminal) },
    { mod = {"Super"},         key = "Space",  action = blink.spawn(blink.config.launcher) },
    { mod = {"Super"},         key = "q",      action = blink.close_focused() },
    { mod = {"Super"},         key = "f",      action = blink.toggle_fullscreen() },
    { mod = {"Super"},         key = "t",      action = blink.toggle_float() },
    { mod = {"Super", "Shift"},key = "r",      action = blink.reload() },
    { mod = {"Super", "Shift"},key = "q",      action = blink.quit() },
}

-- Window rules (per-app overrides)
blink.rules = {
    { class = "Gimp",      floating = true },
    { class = "Pavucontrol", floating = true, size = {600, 400} },
    { class = "firefox",   workspace = 2 },
    { class = "discord",   workspace = 3, opacity = 0.95 },
}

-- Theme (overrides colors.ini if set here)
blink.theme = {
    border         = "#3c3c3c",
    border_active  = "#007ACC",
    background     = "#1e1e1e",
    surface        = "#252526",
    text           = "#cccccc",
    accent         = "#007ACC",
}
```

---

## 16. Recommended Crates

These crates should be added to the workspace `Cargo.toml` in addition to the core dependencies listed in Section 11.

### Workspace-wide (all crates)
```toml
[workspace.dependencies]
# Async runtime
tokio = { version = "1", features = ["full"] }

# Error handling
anyhow = "1"
thiserror = "2"

# Serialization (IPC JSON payloads)
serde = { version = "1", features = ["derive"] }
serde_json = "1"

# Logging
tracing = "0.1"
tracing-subscriber = { version = "0.3", features = ["env-filter"] }

# XDG base directories (~/.config/blink-wm/)
xdg = "2"
```

### blink-wm specific
```toml
# X11 (pure Rust, safe bindings)
x11rb = { version = "0.13", features = ["randr", "xkb", "xinput"] }

# Lua config (replaces rlua — actively maintained, Lua 5.4)
mlua = { version = "0.10", features = ["lua54", "vendored"] }

# File watching (hot-reload colorschemes from pywal/wallust)
notify = "7"
```

### blink-launch / blink-pkg specific
```toml
# Fuzzy search (for app launcher and package search)
fuzzy-matcher = "0.3"

# .desktop file parsing (freedesktop app entries)
freedesktop-entry-parser = "0.5"
```

### Error Handling Strategy
- **Config parse errors**: Log the error with `tracing`, fall back to built-in defaults. Never crash on bad config.
- **X11 connection errors**: Fatal — log and exit cleanly, attempting to unmap all managed windows first.
- **Panic handler**: Register a custom panic hook that calls the X11 cleanup routine before unwinding, ensuring windows are not left in an unmanaged state.
- **IPC errors**: Log and continue — a broken IPC client should never crash the WM.
- **Subprocess failures** (blink-bar, autostart): Log the error, continue running without the failed component.
