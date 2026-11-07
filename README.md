# LEXZYON — Android Game Companion 1.0.0

LEXZYON is an Android app shell built with Kotlin + WebView. It provides an installed-app library, per-app profile labels, device/network information, a reachability history, themes, and an optional root-only display-density control.

## Compatibility target

- Minimum Android: 8.0 (API 26)
- Target / compile SDK: Android 15 (API 35)
- Build toolchain: JDK 17, Android Gradle Plugin 8.7.3, Gradle 8.9

This is a compatibility target, not a claim that every feature has been tested on every device or Android skin.

## Feature status

| Feature | Status |
|---|---|
| First screen setup / access-method selector | UI works; selector is informational except root detection |
| Installed-app library | Reads launcher-visible installed apps; add/remove works locally |
| Per-app profiles | Profile labels are saved locally; they do not tune Android/game engine settings |
| Device HUD | Reads Android version, API, resolution, effective density, and network transport |
| Network history | Runs `InetAddress.isReachable`; this is reachability timing, not a guaranteed ICMP ping or Wi-Fi latency benchmark |
| Themes | Red, white, blue, yellow, black, purple, pink |
| Smooth Drag | Root-only `wm density` override, 320–1440 DPI, with saved original-density backup and restore fallback |
| Shizuku / Wireless ADB / computer ADB | Setup guidance only; no in-app client / Binder integration in this release |
| FPS / CPU temperature / per-process RAM | Not reported; Android does not expose these consistently to ordinary apps |

## Important density safety note

Android's `wm density` is a **device-wide display setting**, not a per-game setting. LEXZYON applies it only when the user starts a selected app and attempts to restore it when the user returns to LEXZYON. If the app is killed, the original value is saved and restoration is retried at the next launch. This is a fallback, **not a guaranteed game-exit monitor**. Check the display after leaving a game and use **Restore original density** if needed. Do not choose an extreme density value; some apps may become difficult to use.

Only use the root option if you understand the system-level effect and explicitly approve the root permission prompt. Without root, the app remains usable in basic mode; density changes will not apply.

## Build APK with GitHub Actions

1. Extract this ZIP.
2. Open the repository: https://github.com/resXite/Lexzyonn
3. Upload the **contents** of the extracted `LEXZYON` folder to the repository root (not the outer folder).
4. Commit to the `main` branch.
5. Open **Actions** → **Build LEXZYON APK**. A push to `main` also starts the workflow.
6. Open the completed run and download the `LEXZYON-debug-apk` artifact.
7. Extract the artifact ZIP; the APK is `app-debug.apk`.

## Local build

Requires JDK 17, Android SDK Platform 35, Build Tools 35.0.0, and Gradle 8.9:

```bash
gradle assembleDebug
```

## Verification status

The inline JavaScript has been syntax-checked. This workspace does not have the Android SDK / Gradle toolchain installed, so an APK compile and device-level test have **not** been performed here. The GitHub repository has not been changed by this workspace. Run the GitHub Actions workflow to get the first compiled APK and inspect its build log.

## Next engineering work (not included in 1.0.0)

- Shizuku API / UserService integration and permission handling.
- A supported Wireless Debugging pairing flow.
- Usage-access-based game session monitoring with Android-version-specific foreground-service handling.
- Device-specific validation for any performance-related controls.
- Release signing and distribution setup.
