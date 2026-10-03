Hega Launcher (v4)
A fully local-running Android home screen launcher.
What's new in this version
Home screen and App Drawer settings are now completely separate. Long-press on a blank area on the Home screen → "Home screen settings". In the App Drawer, tap ⚙ in the top right → "Drawer settings". Icon size, shape, and row/column counts are now independent for both.
Add to Dock is now available in both places: Long-pressing an app on either the Home screen or in the App Drawer now brings up the "Add/Remove from Dock" option.
Dock color and transparency are customizable: Home screen settings → Dock section. Includes 7 color options + a 0-100% opacity slider.
Clock and widgets can now be freely moved/resized:
Long-press on the clock → "Drag to move" (drag it wherever you want with your finger) or "Adjust size".
Long-press on a widget → Move/resize in the same way, or remove it.
You can reset to default using "Reset clock and widget positions" in Home screen settings.
The "Apps top margin" slider allows you to adjust where the Home screen app grid starts (below the clock or right at the top).
Icon shape fix: "Circle" is now a true full circle that fits the square boundary perfectly. In the previous version, some apps' adaptive icons kept their squarish masks and appeared blocky; now icon layers are rendered directly with a true full circular mask applied on top.
Fixes for widget loading issues:
The widget picker list now displays the app ownership and dimensions, making widgets easier to identify.
The binding and configuration flow is now handled directly through the system's native widget host mechanism—replacing the old flow that caused some widgets to fail loading.
If a widget fails to load, it no longer fails silently; a "Failed to load widget" alert appears and incomplete registrations are cleared.
Widget dimensions are now reported accurately based on real system pixel sizes (fixing the issue where some widgets appeared tiny or glitched).
General Features
Horizontal scrolling Home screen + separate App Drawer (opened by tapping the ⠿ button on the right side of the dock), both with page support and folders.
The Home screen starts empty on fresh installation; add items from the Drawer via "Add to Home screen".
Folders, widgets, and wallpaper customization.
Settings: icon shape/size, text size/color, column/row count—configured independently for Home screen and Drawer; plus dedicated clock and dock settings for the Home screen.
Installation / Update
A fixed debug signing key is used (app/debug.keystore, located in the repository). Since the versionCode increments with each update, you can install directly over the previous version.
Upload this zip to the repository (overwrites the old one).
Actions → Build APK → Run workflow.
Once completed, download app-debug from Artifacts and install the .apk.
Settings → Apps → Default apps → Home app → Select Hega Launcher (no need to reselect if already set).
Limitations
No drag-and-drop between pages; items are sorted by addition/alphabetical order.
Supports only one widget slot at a time.
Icon packs are not supported.
If you encounter an issue, share a screenshot of any line starting with "e:" in the "Build" step logs for the fastest resolution.
v6: Rearranging Items
In the Home screen, App Drawer, and Dock, you can long-press an app or folder and select "Change position". Tapping the next app or folder swaps their positions. You can repeat this process as many times as you like to fully customize your layout. Changes are saved permanently.
Note: This is not a drag-and-drop interface; it operates on a "select → tap target → swap" model (requiring two taps to move an item). If you prefer continuous touch drag-and-drop, request it as a separate feature.
What's Next
Upcoming plans alongside this update include three separate standalone apps:
Hega Music, Hega Video, and Hega Photos—plus support for 5 languages (English, Spanish, French, Arabic, and Persian). Due to the large scope, these will be released in separate updates.
v6.1: Hega Music
A dedicated music player embedded within Hega Launcher that does not automatically appear in the Home screen or App Drawer grid.
How to open:
Long-press a blank area on the Home screen or Drawer → "Settings" → tap the "Open Hega Music" button at the top.
Once opened, you can pin it to the main screen via its own ⋮ menu → "Add to Home screen"—removing the need to go back into Settings.
Features:
Tapping Scan requests storage permissions ("Music and Audio" permission on Android 13+); once granted, it scans all tracks on the device and lists them with cover artwork and titles.
⋮ menu → Storage Location: Options for Internal Storage / SD Card / USB (OTG). Selecting an unmounted volume triggers a "Volume not mounted" alert; if connected, it scans that specific directory. (Note: Distinguishing between SD Card and OTG is not natively flagged in the Android API; if two external drives are detected, the first is treated as SD Card and the second as OTG. Let us know if this appears inverted on your device).
Tapping a track opens a player UI styled similarly to YouTube Music: album art, title/artist, progress bar, shuffle/previous/play-pause/next/repeat controls. Dislikes/likes row excluded as requested.
Tapping back (⌄) returns to the library while audio continues playing (note: background notification/mini-player controls are not yet implemented; playback stops if the app is fully closed or the screen sleeps, which will be addressed in a future update).
No editing options included as per design—strictly focused on scanning, listing, and playback.
v6.2: Background Playback + Hega Photos
Background Playback: Hega Music now runs via a foreground service (with notification integration). Playback continues when leaving the app or turning off the screen; previous/play-pause/next controls are available directly from the notification shade and lock screen. Requests notification permission on first play in Android 13+. Reopening Hega Music displays the currently playing track.
Hega Photos (Access mechanism matches Hega Music: Hidden from Drawer; access via Settings → "Open Hega Photos" or pin via its ⋮ menu → "Add to Home screen"):
Scan → Storage permission → Displays photos in a 3-column grid.
Tapping a photo opens a MIUI Gallery-style viewer: displays date/time at the top, with Share / Edit / Delete / Details options at the bottom. Swipe left/right to navigate between photos.
Edit: Crop (drag handles/inside grid, "Apply crop"), Pen (7 color presets, stroke size, opacity slider), and Eraser (size, strength controls—erases drawing overlays only, keeping the original photo intact). Saving overwrites the original file (prompts native Android system confirmation).
Delete and Details (file name, resolution, file size, date, format, location metadata).
Video (Hega Video) and 5-language localization remain pending development.
Known limits: No pinch-to-zoom in the viewer; editing resolution capped at ~2400 px max; SD/OTG selection is currently unavailable in Photos (supported in Music).
