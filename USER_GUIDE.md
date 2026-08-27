# Heaven Cast 1.0 - Streamer Guide

## 1. Install and start

### Installer

Run `Heaven Cast Setup 1.0.0.exe`, choose an installation folder, and launch Heaven Cast from the Start menu or desktop shortcut. You'll be asked to accept the license terms before installation continues.

### Portable

Extract the entire ZIP to a normal folder, then run `Heaven Cast.exe`. Do not run the executable from inside the ZIP.

Windows may show a SmartScreen warning because this release is not code-signed. Confirm that the file hash matches `SHA256SUMS.txt` before choosing **More info -> Run anyway**.

Heaven Cast minimizes to the system tray when its window is closed. Use the tray icon and choose **Quit** to stop it completely. The tray menu also has a **Live Preview** entry (see section 2).

## 2. Connect OBS Studio

1. Open the Heaven Cast control room.
2. Copy the Browser Source URL shown in **Connect OBS Studio**.
3. In OBS, add a **Browser Source**.
4. Set the URL to `http://127.0.0.1:5310/broadcast`.
5. Set the canvas to **1920 x 1080**.
6. Leave Custom CSS empty.

The source is transparent and is designed to sit above the Umamusume window capture. Use the control-room safe-area, scale, opacity, and side controls instead of transforming individual overlay panels in OBS.

**Live Preview** (next to the Browser Source URL, and in the tray menu) opens a full-screen, click-through window showing the overlay directly over the running game, at full resolution — closer to what a viewer actually sees than the small OBS preview panel. It assumes the game fills the primary display; if you run Umamusume in a window rather than full screen, the preview won't line up with it. Click the button again (or the tray entry again) to close it. It doesn't intercept mouse or keyboard input, so it's safe to leave open while you play.

## 3. The control room at a glance

The three status cards (Umamusume installation, runner portraits, replay telemetry) show whether each piece is ready. **Start race link** connects the telemetry bridge to the game; **Stop** disconnects it. With **Automatic race link** checked (in the row below the OBS panel), Heaven Cast connects on its own whenever Umamusume is running and reconnects if the game restarts — you normally don't need to touch Start/Stop manually.

**Check for updates** (on the portraits card) re-scans the installed game's asset catalog and rebuilds the local portrait/icon set if anything changed. This happens automatically after a game update too; the button is there for forcing it or checking status.

**Native Game HUD** temporarily brings back Umamusume's own on-screen controls, which Heaven Cast otherwise hides once a race starts. You need this to reach the game's own race-skip button. Toggle it again to return to the clean broadcast view — it also has a configurable global hotkey (section 4).

The **Activity** panel at the bottom is a running log of what the telemetry bridge is doing (connecting, capturing a replay, resolving trainer clubs, HUD state). It's there for troubleshooting, not something you need to watch during a normal race.

## 4. Select runners and global hotkeys

Click a runner in the control room (while a race is loaded) to feature their detailed telemetry on the overlay. The selection stays fixed until you pick another runner, until automatic rotation or camera-follow picks up again (section 5), or until you use a hotkey.

Three global hotkeys are available, none set by default:

- **Previous Uma** — moves the featured selection up through the live ranking.
- **Next Uma** — moves it down through the live ranking.
- **Toggle Native HUD** — same as the Native Game HUD button in section 3.

To set one, click its button under **Global hotkeys** and press the key combination you want (a single key, or with Ctrl/Alt/Shift held). **Clear** removes it. These are global — they work even when Umamusume has focus, not just when the control room window does — so pick something that isn't going to double as an in-game shortcut. If a hotkey shows as unavailable, another application already has it registered; pick a different combination.

## 5. Automatic direction

Three switches under **Live direction** decide who gets featured and what commentary shows up, without you touching anything mid-race:

- **Auto Director** is the general switch for the editorial read of the race — skill activations and battles for position. Turn it off and the Race Watch ticker and the leader/battle/skill cards stop appearing entirely, regardless of the module toggles in section 6. Leave it on and use the module toggles there for finer control over which of the two panels shows.
- **Auto Rotate Top 5** cycles the featured-runner panel through the current top five, one every 8 seconds. Picking a runner manually (click or hotkey) pauses rotation for a few seconds before it resumes from wherever you left it.
- **Follow Game Camera** keeps the featured panel on whichever runner Umamusume's own commentary camera is currently focused on. It takes priority over Auto Rotate while it's on. A manual pick still holds briefly before camera-following resumes, same as with rotation.

Auto Rotate and Follow Game Camera are mutually exclusive in practice — whichever is driving the selection wins. Turning both off leaves the last manually selected runner pinned indefinitely.

## 6. Visible modules

These toggles control what appears on the actual broadcast output. Each one hides its panel entirely rather than leaving an empty space.

- **Race header** — the top bar: race title, track, weather, distance, and a progress rail.
- **Live ranking** — the live position list on the left (or right, see section 7), with each runner's gap, trainer, running style, and position-change arrow.
- **Race Watch** — the narrative ticker describing what's happening right now (new leader, tightening gap, and so on). Also gated by Auto Director above.
- **Editorial events** — the leader / battle-for-position / skill-activated / closing-fast cards. Also gated by Auto Director above.
- **Runner detail** — the featured runner's full card: portrait, position/speed/stamina/gap stats, and the four items below. Turning this off removes the card entirely, which also hides everything in the next four items regardless of their own state.
- **Performance charts** — the speed and position history sparklines inside the detail card.
- **Latest skill** — the most recently activated skill (icon, name, timestamp) inside the detail card.
- **Player and club** — trainer name and club, shown both in each ranking row and in the detail card.
- **Position changes** — the up/down arrow and count next to each runner's position in the ranking list.

## 7. Layout and readability

- **Overlay side** — puts the ranking list and Race Watch panel on the left or right of the canvas.
- **Density** — Comfortable is the default spacing; Compact tightens row height in the ranking list.
- **Text size** — Normal or Large, affects the featured runner's name and identity text.
- **Global scale** (70%-130%) — scales the whole overlay up or down, useful if your canvas or safe areas differ from the standard 1920x1080.
- **Panel darkness** (40%-100%) — background opacity of the panels; lower values let more of the game show through behind them.
- **Accent color** — the highlight color used across badges, active states, and progress indicators.

Changes here don't take effect until you click **Save and apply**. **Reset to default** restores the built-in Default Broadcast values for the currently open profile without needing a new one.

## 8. Profiles

A profile bundles every setting in sections 5 through 7, plus module visibility, under one name. Use the selector at the top of the control room to switch between them, **New** to start a clean one, **Duplicate** to branch off the current one, and **Delete** to remove one (you always need at least one profile left). Switching profiles applies immediately; the overlay updates without needing to touch the OBS Browser Source URL, since it always reflects whichever profile is active.

This is useful for keeping, say, a minimal layout for casual races and a fuller one for tournament broadcasts, without rebuilding settings each time.

## 9. Portraits and icons

The installer and portable package already contain the release portrait, NPC, rank, and skill-icon catalogs. No separate asset folder is required.

On startup, Heaven Cast compares its catalog with the installed game's manifest. After a game update, it automatically rebuilds the local portrait catalog when necessary. You can also select **Check for updates** in the control room. The update uses files from your own local Umamusume installation and does not download them from a cloud service.

## 10. Troubleshooting

### The control room does not open

Check the system tray first. Only one Heaven Cast instance can run. Quit the existing tray instance and start it again.

### OBS shows a blank source

Confirm that Heaven Cast is running, refresh the Browser Source, and verify the URL and 1920 x 1080 dimensions. The overlay is intentionally transparent when no scene element occupies an area.

### Telemetry says waiting

Start Umamusume and enter a new 3D race. If the game was already inside a race when Heaven Cast restarted, begin another race so the complete replay can be captured.

### A global hotkey is unavailable

Another application has reserved that key. Choose a different key in the control room.

### Portrait update fails

Confirm that the global Umamusume installation is present and fully updated. Retry **Check for updates** after closing any application that may be scanning the game files.

## 11. Privacy and local services

Heaven Cast uses only localhost services:

- control room and OBS output: `127.0.0.1:5310`;
- internal telemetry: UDP `127.0.0.1:5312`;
- internal HUD control: UDP `127.0.0.1:5313`.

No race telemetry is uploaded by the application.
