# Liquid Glass Music — Android app

A minimal Android Studio project that wraps your `liquid-glass-music-widget.html`
in a full-screen WebView, so it runs as a native-feeling Android app instead of
a browser tab. The HTML/CSS/JS itself is untouched — it's just bundled as an
asset (`app/src/main/assets/index.html`) and loaded edge-to-edge.

## How to build it

You'll need [Android Studio](https://developer.android.com/studio) (free) —
that's the easiest path since it handles the Gradle wrapper and SDK downloads
for you.

1. Unzip this project.
2. Open Android Studio → **Open** → select the unzipped `LiquidGlassMusicWidget` folder.
3. Let it sync (first sync downloads Gradle + the Android SDK bits it needs —
   this project didn't ship the Gradle wrapper jar, so Android Studio will
   offer to generate one automatically; accept that prompt).
4. Plug in an Android phone (with USB debugging on) or start an emulator.
5. Click **Run ▶**.

That produces a real installable app. To get a shareable APK without a device:
**Build → Build Bundle(s) / APK(s) → Build APK(s)**, then find it under
`app/build/outputs/apk/debug/app-debug.apk`.

## What's in here

- `app/src/main/assets/index.html` — your original widget file, byte-for-byte.
- `MainActivity.kt` — a WebView with JS/DOM storage enabled, drawn edge-to-edge
  so the gradient background fills the whole screen behind the status/nav bars.
- Minimal launcher icon + theme so it looks like a real app in the app drawer.

## Notes

- The widget's Google Fonts (`fonts.googleapis.com`) load over the network, so
  the manifest requests `INTERNET` permission. Everything else in the widget
  (drag-to-move, the customization panel, settings copy/paste) is local JS —
  no other permissions are needed.
- `minSdk` is set to 26 (Android 8.0+), which covers the vast majority of
  active devices and keeps the adaptive-icon setup simple.
- This is a plain WebView wrapper, not a native rewrite — every visual detail
  (the SVG refraction filter, drag physics, customizer) is the exact code you
  uploaded, just running full-screen in its own app instead of a browser tab.
