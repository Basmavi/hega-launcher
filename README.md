Hega Launcher (v4)
A fully local Android home screen launcher.
What's New in This Version
Home screen and App Drawer settings are now completely separate: Long-press on an empty area on the Home Screen → "Home screen settings". Tap the ⚙ icon in the top right of the App Drawer → "Drawer settings". Icon size, shape, and row/column counts are now independent for both.
"Add to Dock" is now available in both places: Long-pressing an app on either the Home Screen or in the App Drawer brings up the "Add/Remove from Dock" option.
Customizable Dock color and transparency: Home Screen Settings → Dock section. Offers 7 color choices + a 0–100% opacity slider.
Clock and widgets can now be freely moved and resized:
Long-press the clock → "Drag to move" (drag anywhere with your finger) or "Adjust size".
Long-press a widget → Move, resize, or remove it in the same way.
Reset to default anytime using "Reset clock and widget positions" in Home Screen Settings.
Use the "Top padding for apps" slider to set where the app grid begins on the home screen (directly below the clock or right from the top).
Icon shape fix: "Circle" is now a true pixel-perfect circle fitting the square mask. In previous versions, some apps' adaptive icons retained their default squircle masks; now, icon layers are rendered directly with a precise circular mask applied on top.
Fixes for widget loading issues:
The widget picker list now displays the parent app name and dimensions, making widgets easier to identify.
The binding and configuration flow now runs through the system's native widget host framework, replacing the legacy flow that caused certain widgets to fail to load.
If a widget fails to load, it no longer fails silently; a "Failed to load widget" alert appears and incomplete records are cleaned up.
Widget dimensions are now accurately reported to the system based on actual pixel size, fixing issues where widgets appeared tiny or distorted.
General Features
Horizontal scrolling Home Screen + separate App Drawer (opened by tapping the ⠿ button to the right of the dock), both with paginated layouts and folder support.
The Home Screen starts empty on fresh installation; add apps manually from the App Drawer via "Add to home screen".
Supports folders, widgets, and custom wallpaper changes.
Settings: Custom icon shape/size, font size/color, column/row counts (independent for Home Screen and Drawer), alongside clock and dock settings for the Home Screen.
Installation / Updating
Uses a fixed debug signing key (app/debug.keystore in the repository). Since versionCode increments with each update, you can install it directly over previous builds.
Upload this zip file to the repository (overwrites the old file).
Go to Actions → Build APK → Run workflow.
Once complete, download app-debug from Artifacts and install the .apk.
Go to Settings → Apps → Default apps → Home app → Select Hega Launcher (no need to reselect if already set).
Limitations
No cross-page drag-and-drop; items are ordered alphabetically or by addition order.
Supports only one active widget area at a time.
Icon packs are not supported.
If an error occurs during build, take a screenshot of any line starting with "e:" in the "Build" step logs for quick troubleshooting.
v6: Swap Position
Long-press any app or folder on the Home Screen, App Drawer, or Dock and select "Swap position". Tap any second app or folder to swap their locations. Repeat as needed to organize your layout; all changes are saved permanently.
Note: This operates as a "select → tap target → swap" mechanism rather than direct drag-and-drop. If you prefer continuous touch drag-and-drop, submit a feature request and it can be added in a future update.
What's Next
The roadmap includes three standalone companion apps—Hega Music, Hega Video, and Hega Photos—along with multi-language support for 5 languages (English, Spanish, French, Arabic, and Persian). Due to their scope, these will be rolled out across separate updates.
v6.1: Hega Music
An isolated music player embedded within Hega Launcher that remains hidden from the default Home Screen and App Drawer listings.
How to open:
Long-press an empty area on the Home Screen or App Drawer → "Settings" → Tap "Open Hega Music" at the top.
Once opened, tap the ⋮ menu inside Hega Music and select "Add to home screen" to pin a shortcut for quick access.
Features:
Tapping Scan requests storage permissions (or "Music and Audio" permission on Android 13+), scanning local storage to index all tracks complete with album art and metadata.
⋮ Menu → Storage Location: Switch between Internal Storage, SD Card, and USB (OTG). Selecting an unmounted volume displays a "Volume not mounted" notification. (Note: Android APIs do not strictly differentiate between SD Cards and OTG drives via distinct flags; if two external drives are detected, the first is assigned as SD Card and the second as OTG).
Tapping a track launches a player UI modeled after YouTube Music: displays album artwork, track/artist info, progress bar, and controls for shuffle, skip back, play/pause, skip forward, and repeat. Does not include like/dislike buttons.
Tapping back (⌄) returns to the library while playback continues in the foreground. (Background playback notification service is planned for a future update; quitting the app or locking the screen currently pauses playback).
No editing support—focuses strictly on scanning, organizing, and playback.
v6.2: Background Playback + Hega Photos
Background Playback: Hega Music now runs via a foreground service with media notifications. Playback continues uninterrupted when exiting the app or turning off the screen. Media controls (previous, play/pause, next) are accessible directly from the notification shade and lock screen. Requests notification permissions on first launch in Android 13+. Reopening Hega Music displays the currently playing track.
Hega Photos (Hidden from the App Drawer; access via Settings → "Open Hega Photos" or pin to Home Screen via its ⋮ menu):
Scan → Grants storage access → Displays images in a 3-column grid layout.
Tapping an image opens a MIUI Gallery-inspired viewer displaying date/time at the top and Share / Edit / Delete / Details options at the bottom. Swipe left/right to navigate between photos.
Edit: Includes Crop (drag edges/corners + "Apply Crop"), Brush Tool (7 color presets, stroke size, transparency slider), and Eraser (adjustable size and opacity; removes drawn annotations only without altering the underlying image). Saving overwrites the original file (requires Android system write confirmation).
Delete and Details views (displays filename, resolution, file size, date, file format, and GPS location data).
Hega Video and 5-language localization remain in development.
Known Limitations: No pinch-to-zoom support in the photo viewer; image editing canvas capped at ~2400px resolution; SD/OTG storage target selection currently exclusive to Hega Music.
v6.3: Hega Video, Widgets, Theme Support
Hega Video (Hidden from App Drawer; access via Settings → "Open Hega Video" or pin via its ⋮ menu): Scan → Storage Permission → Video Grid (displays thumbnail preview, duration, and file size). Tapping plays video with playback controls (play/pause, seek bar). Supports uninterrupted screen orientation changes and keeps the screen awake during playback. Includes Delete and Details views; editing is not supported.
Standalone App Widgets: Hega Music, Hega Photos, and Hega Video appear as individual widgets in the Android system widget picker (compatible with all third-party launchers, including MIUI Launcher). Add multiple instances independently; tapping launches the target application. Fully resizable.
Unlimited Widgets in Hega Launcher: Long-press empty space on the Home Screen → "Add Widget" can be executed indefinitely. Long-press any placed widget to move, resize, reset, or remove it. Legacy single-widget configurations auto-migrate to the new multi-widget layout.
Theme Engine: Settings → Theme → Light / Dark mode toggles. System dialogs, Settings, Music, Photos, and Video UIs adapt to the selected theme (the photo editor UI remains permanently dark). Home Screen and App Drawer font colors remain customizable via their respective color options to maintain visibility over custom wallpapers.
Coming Soon: Hega Browser, followed by internationalization (Turkish + 5 language options).
