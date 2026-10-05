# Hega Launcher

A fully local Android home-screen launcher with a built-in suite of small apps:
**Hega Music**, **Hega Photos**, **Hega Video** and **Hega Browser**.

- **Version:** 6.4 (`versionCode` 10)
- **Minimum Android:** 8.0 (API 26) · **Target:** Android 14 (API 34)
- **Language of the UI:** Turkish (English, Spanish, French, Arabic and Persian are planned)
- **Written in:** Kotlin, plain Android Views, no third-party UI libraries

---

## Features

### Launcher
- **Swipeable home screen** with pages, page dots and a bottom **dock** (up to 5 apps).
- The home screen **starts empty**. You add apps and folders yourself from the App Drawer.
- **App Drawer** (round button at the right end of the dock): all apps and folders on
  swipeable pages, with search and its own settings.
- **Folders:** long-press an app in the drawer → *Move to folder*.
- **Rearranging:** long-press an item → *Change position*, then tap the item to swap with.
  Works on the home screen, in the drawer and in the dock.
- **Unlimited widgets** on the home screen. Each widget can be dragged, resized, reset or
  removed individually (long-press it). 1x1 widgets are sized as true 1x1 cells.
- **Movable and resizable clock** (or hide it completely).
- **Icon shapes:** square (slightly rounded), perfect circle, squircle.
- **Appearance settings, separately for Home and Drawer:** icon size, label size and colour,
  number of columns and rows per page. Dock colour and opacity are adjustable.
- **Wallpaper** is changed through the system picker.
- **Light / dark theme** (Settings → Theme).
- Always draws edge-to-edge behind transparent system bars.

### Hega apps (hidden from the drawer on purpose)
The four apps below are registered as real launchable activities with their own icons, but
the Hega App Drawer deliberately does **not** list them. Open them from
*Settings → Hega Apps*, or open one once and use its **⋮ menu → Add to home screen**.

| App | What it does |
| --- | --- |
| **Hega Music** | Scans music (internal storage / SD card / USB-OTG), shows covers and titles, YouTube-Music-style player (shuffle, previous, play/pause, next, repeat), **keeps playing in the background** with a media notification and lock-screen controls. No editing. |
| **Hega Photos** | Photo grid, gallery-style viewer (share, edit, delete, info, swipe between photos). Editor with **crop**, **pen** (colour / size / opacity) and **eraser** (size / strength). |
| **Hega Video** | Scans videos, plays them (rotation-safe, keeps the screen on), delete and info. No editing. |
| **Hega Browser** | WebView-based, single tab: address/search bar, back / forward / home / reload, bookmarks, history, downloads, desktop-site mode, search engine choice (Google, DuckDuckGo, Bing), fullscreen video, file upload, share, clear browsing data. Can also be chosen to open `http(s)` links. |

### Widgets for other launchers
Hega Music, Hega Photos, Hega Video and Hega Browser each provide a **1x1 app widget**
(resizable). They appear in the widget picker of any launcher — including MIUI's — and you
can add as many as you like. Tapping one opens the app.

---

## Permissions

| Permission | Why |
| --- | --- |
| `QUERY_ALL_PACKAGES` | A launcher has to list all installed apps and widget providers. |
| `READ_MEDIA_AUDIO` / `READ_MEDIA_IMAGES` / `READ_MEDIA_VIDEO` (Android 13+), `READ_EXTERNAL_STORAGE` (Android ≤ 12) | Hega Music / Photos / Video scan your media. Requested only when you tap *Scan*. |
| `FOREGROUND_SERVICE`, `FOREGROUND_SERVICE_MEDIA_PLAYBACK`, `POST_NOTIFICATIONS` | Background music playback and its notification. |
| `INTERNET` | Used **only** by Hega Browser. The launcher and the other apps do not use the network. |
| `WRITE_EXTERNAL_STORAGE` (Android ≤ 9 only) | Browser downloads on old Android versions. |

There is no analytics, no tracking and no account. Settings, folders, bookmarks and history
are stored locally in `SharedPreferences`.

---

## Using it

1. Install the APK and set **Hega Launcher** as the default home app
   (*Settings → Apps → Default apps → Home app*).
2. Open the drawer (round button, bottom right), long-press an app → *Add to home screen*.
3. Long-press an empty area of the home screen for wallpaper, settings, clock and widgets.
4. Long-press an app → *Add to dock*, *Change position*, *Move to folder*, *App info*, *Uninstall*.

On MIUI also allow *Autostart* and set battery saver to *No restrictions* for Hega Launcher,
otherwise background music may be stopped by the system.

---

## Building

### Android Studio
1. *File → Open* the project folder (the one containing `settings.gradle`).
2. Let Gradle sync (needs internet once), then press **Run**.

### GitHub Actions (no computer needed)
Add this file as `.github/workflows/build.yml`, then run it from the **Actions** tab:

```yaml
name: Build APK
on: workflow_dispatch
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: '17'
      - uses: gradle/actions/setup-gradle@v3
      - name: Build
        run: gradle assembleDebug
      - uses: actions/upload-artifact@v4
        with:
          name: app-debug
          path: app/build/outputs/apk/debug/app-debug.apk
```

(If you keep the whole project zipped in the repository, add an `unzip HegaLauncher.zip`
step and set `working-directory: HegaLauncher` on the build step.)

### Updating in place
`app/debug.keystore` is committed on purpose: every CI build is signed with the same key, so a
new APK installs **over** the old one without uninstalling and without losing your data.
Always increase `versionCode` in `app/build.gradle` for a new release.

---

## Project layout

```
app/src/main/java/com/ismail/launcher/
  MainActivity            home screen (pages, dock, clock, widgets)
  AppDrawerActivity       app drawer with search and folders
  SettingsActivity        settings (separate for Home and Drawer)
  LauncherPrefs           all launcher settings (SharedPreferences + JSON)
  IconShaper, FolderIcon  icon masking and folder previews
  DragLayout              movable container used for clock and widgets
  MusicActivity / MusicService / MusicScanner / SongAdapter
  PhotoActivity / PhotoEditView / PhotoScanner / PhotoAdapter
  VideoActivity / VideoScanner / VideoAdapter
  BrowserActivity / BrowserStore
  AppShortcutWidgets      the four 1x1 app widgets
  ThemeHelper             light / dark theme selection
```

---

## Known limitations

- Rearranging is "pick, then tap the target to swap" — not finger drag-and-drop.
- Hega Browser has a single tab and no private mode.
- Hega Photos has no pinch-to-zoom in the viewer; the editor works on a downscaled copy
  (longest side ≤ ~2400 px) and saving overwrites the original file.
- Hega Music keeps no queue/playlists; it plays the list from the last scan.
- SD card vs. USB-OTG detection depends on what Android reports; with two removable volumes
  the first is treated as the SD card and the second as OTG.
- No icon-pack support.

## Roadmap

- UI languages: English, Spanish, French, Arabic (RTL) and Persian (RTL), next to Turkish.
- Browser tabs.
