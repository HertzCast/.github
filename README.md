# .github
# HertzCast

<p align="center">
  <img src="screenshots/hertz_logo.png" width="100" alt="App Icon" />
</p>

A native macOS application for controlling **Yamaha AV receivers** over your local network — no third-party apps, no subscriptions, no cloud.

**Website:** [thedanbutuc.github.io/HertzCast](https://thedanbutuc.github.io/HertzCast/)

<p align="center">
  <img src="screenshots/UI 1.png" height="450" alt="Main UI — Net Radio Now Playing" />
  &nbsp;&nbsp;
  <img src="screenshots/UI 6.png" width="300" alt="Menu Bar Mini Player" />
</p>

<p align="center">
  <img src="screenshots/UI 3.png" height="450" alt="Audio Settings" />
  &nbsp;&nbsp;
  <img src="screenshots/UI 4.png" height="450" alt="Settings" />
</p>

<p align="center">
  <img src="screenshots/UI 5.png" height="450" alt="Zone 2" />
  &nbsp;&nbsp;
  <img src="screenshots/UI 2.png" height="450" alt="Music Center" />
</p>

---

## Features

### Receiver Display
A retro LCD-style panel shows real-time receiver state, rendered in **Bitcount Prop Single ExtraLight** — a bitmap display font that matches the aesthetic of real audio equipment. The panel has a fixed size regardless of input source — layout never shifts when switching between sources.
- **Signal format** — audio codec, bit depth, and sample rate shown centered at the top when available (e.g. `PCM · 16-BIT · 44.1 KHZ`, `AAC · 320 KBPS · 44.1 KHZ`, `DOLBY DIGITAL PLUS · 48 KHZ`)
- **Current input source** — large phosphor-style display
- **Volume** — updates live in dB while dragging the knob; raw value as fallback
- **Sound mode** — DSP/surround program (Straight, Stereo, Surround Decoder, etc.)
- **Shuffle / Repeat indicators** — appear between the volume and mode readouts when active; `⇄` for shuffle, `↻` for repeat all, `↻1` for repeat one
- **Now Playing** — for Spotify and Net Radio inputs, shows the current track title and artist/station name, refreshed every 8 seconds; long names scroll continuously in a right-to-left marquee loop
- **Album art** — thumbnail with accent-colored border displayed for Spotify (always) and Net Radio (when the station provides it); gracefully falls back to text-only layout when unavailable
- **Mute indicator** — highlighted in red when active
- **Favourites heart** — while on Net Radio, a heart icon appears below the station name. Filled accent-colored heart = station is already saved in presets; empty heart = not yet saved. Tap to add or remove from Favourites instantly; shows an alert if all preset slots are full

### Power Control
A compact metallic circular button controls the receiver power state:
- Tap to toggle between **On** and **Standby**
- White power icon; glows with the accent color when the receiver is on
- Animated press feedback
- **Last-source restore**: powers back on to whichever input was active before standby

### Volume Control
A rotating metallic knob controls the receiver volume:
- **Graduation ring** — 31 tick marks around the knob, lit with the accent color up to the current level; MIN / MAX labels at the endpoints
- **Drag** to set volume — circular arc gesture; the knob rotates and the receiver volume changes in real time while dragging, with a single API call per integer step
- **Scroll wheel** — mouse wheel and trackpad both work
- **Keyboard shortcuts** — `Cmd ↑` / `Cmd ↓` volume up/down, `M` toggle mute, `P` play/pause, `S` shuffle, `R` repeat cycle, `Cmd ←` previous, `Cmd →` next

### Header Controls
Four metallic circular buttons in the window header — same design as the Mute button — give access to side panels:
- **Zone 2** (`⊟`) — open/close the Zone 2 panel
- **Music Center** (`♫`) — open/close the Music Center panel
- **Audio Settings** (`≡`) — open/close the Audio Settings panel
- **Settings** (`⚙`) — open/close the Settings panel
- Active panel button glows with the accent color; inactive buttons show white

### Mute
A dedicated Mute button sits next to the volume knob:
- White speaker icon; glows with the accent color when muted
- Toggles mute state on the receiver

### Input Source Buttons
Four physical keycap-style buttons for quick source switching, fully configurable in Settings:
- White label when inactive; accent-colored with a glow when active
- LED indicator dot below each button
- **Power-on shortcut**: tapping a source button while standby powers on directly to that source
- State syncs with the receiver within a few seconds

### Transport Controls
A compact set of transport buttons:

| Row | Buttons | Action |
|-----|---------|--------|
| 1 | `⇄` `⏮` `▶` `⏭` `↻` | Shuffle toggle / Previous / Play / Next / Repeat cycle |
| 2 | `<<` `■` `‖` `>>` | Tune − / Sound mode cycle / Band toggle (FM↔AM) / Tune + |
| 3 | `<` `>` | Preset − / Preset + |

Context-sensitive: `■` stops playback on streaming sources and cycles the sound program on Tuner; `‖` pauses on streaming and toggles FM/AM on Tuner; `< >` cycle through net presets on Net Radio and switch tuner presets on Tuner.

### Audio Settings
A dedicated panel (accessible via the sliders icon in the header) exposes the full YXC audio processing chain:
- **Subwoofer Volume** — slider from −12 to +12; double-click to reset to 0
- **Bass** — tone control bass slider from −12 to +12
- **Treble** — tone control treble slider from −12 to +12
- **Dialogue Level** — four metallic buttons (0–3) with active glow
- **Audio Features** — four toggle buttons on one row: Pure Direct / Enhancer / Extra Bass / Adaptive DRC
- **Sound Program** — full list fetched dynamically from the receiver via `getSoundProgramList`
- **Surround Decoder** — dropdown visible only when Sound Program is set to Surround Decoder

### Music Center
A panel (accessible via the music notes icon in the header) that slides in from the right, mutually exclusive with the other panels:
- **Recent Played** — list of recently played Net Radio stations; tap to recall and play. Each station has a heart button: tap to save it as a preset (plays it first, then stores), or remove it if already saved
- **Favourites** — receiver presets with accent-colored number badges (slot count read dynamically from the receiver — no fixed limit); tap to switch to Net Radio and recall preset. Each favourite has a filled heart; tap to remove it from presets. Right-click for a Delete context menu
- **Net Radio Browser** — full hierarchical browser for the Net Radio directory tree; navigate folders, search within any level, and tap a station to play instantly
- **Sources** — all available receiver inputs with SF Symbol icons; active source highlighted; tap to switch
- **Visible Sources** — toggle individual inputs on/off; hidden sources disappear from the Sources list
- All sections are collapsible `DisclosureGroup` menus with persistent open/closed state

### Theme
A pill-shaped Moon/Sun toggle in Settings switches between **Dark** and **Light** mode:
- **Dark mode** — green accent color, phosphor-style LCD, dark surfaces, glowing LEDs
- **Light mode** — red accent color, bold LCD font, light surfaces, no halos or glows

<p align="center">
  <img src="screenshots/UI Dark.png" height="450" alt="Dark Mode" />
  &nbsp;&nbsp;
  <img src="screenshots/UI Light.png" height="450" alt="Light Mode" />
</p>

### Schedule
Three schedule controls grouped in a collapsible section in Settings:

**Morning Alarm** — automatically powers on the receiver at a scheduled time:
- Enable/disable toggle
- Hour and minute picker
- **Day-of-week selector** — toggle individual days (Mo Tu We Th Fr Sa Su)
- **Source selector** — all supported YXC input sources
- **Preset picker** (1–5) for Net Radio
- **Wake volume** — set the volume level the receiver powers on at; separate from the current volume
- Managed via a background **Login Item** (`HertzCastHelper`) — fires even after Mac sleep/wake

**Auto Off** — automatically puts the receiver in standby at a scheduled time:
- Enable/disable toggle
- Hour and minute picker
- **Day-of-week selector** — same per-day granularity as Morning Alarm

**Sleep Timer** — turns the receiver off after a set time:
- Picker: Off / 15 / 30 / 45 / 60 / 90 / 120 minutes
- Applied instantly to the receiver; resets to Off on next power cycle

### Receiver Discovery
Automatically finds Yamaha receivers on the local network using Bonjour/mDNS:
- **Discover Receiver** button scans and verifies devices via the YXC API
- Auto-selects when exactly one receiver is found; shows a list for multiple
- Manual IP entry available as fallback

### Zone 2
A dedicated panel (accessible via the zone icon in the header) for controlling a secondary audio zone:
- **Power** — On/Standby button in the Zone 2 panel header, same design as the main power button
- **Input** — switch the Zone 2 input source independently
- **Volume** — slider + −/+ buttons; displays level in dB
- **Mute** — toggle Zone 2 mute
- Polled every 3 seconds; available on any Yamaha receiver with Zone 2 hardware output

### Menu Bar Mini Player
Clicking the menu bar icon opens a compact mini player instead of the full UI:
- Album art thumbnail + scrolling track title and artist name (Core Animation marquee)
- Playback controls: Previous / Stop / Play-Pause / Next / Shuffle / Repeat — keycap style matching the main UI
- Volume: − / dB label / + buttons + Mute
- Quit button
- Falls back gracefully when receiver is off or no track is playing

### Notifications
macOS notification when the receiver is turned on or off automatically by a schedule.

### Device Management
- **Reboot Receiver** — button at the bottom of Settings with confirmation dialog; sends `GET /system/requestSystemReboot` to restart the receiver remotely
