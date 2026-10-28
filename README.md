# Second Brain 🧠

A personal second-brain app with Claude AI built in: notes, tasks, journal, tags, linked notes, files (photos, videos, PDFs), and an AI that organizes, extracts and remembers. Data stays on your device and works offline.

## Install

- **Android app:** download [second-brain.apk](https://github.com/khalil203/second-brain/releases/latest/download/second-brain.apk) and open it (allow "Install unknown apps" for your browser when asked).
- **Web app:** open https://khalil203.github.io/second-brain/ in Chrome, then menu ⋮ → **Install app**.

## Updates

The app checks GitHub for new versions and downloads them by itself (Settings → Updates). Tap **Restart** when it says an update is ready. Your notes are never touched by updates.

## Releasing a new version

1. Edit `app.html` and raise `APP_VERSION` (for example `3.0.0` → `3.1.0`).
2. Put the same number in `version.json` → `"version"`.
3. Commit and push to `main`. Phones pick it up through the update button.

Only when the Android shell itself changes (new plugins, icon, app name): raise `apk_version` in `version.json` and in `index.html` (`SB_SHELL.apk`), and add `[apk]` to the commit message. GitHub Actions builds a new signed APK release.

## Files

| File | What it is |
|---|---|
| `app.html` | The whole app |
| `index.html` | Loader that runs the newest downloaded version |
| `version.json` | Latest version numbers, read by the update button |
| `sw.js`, `manifest.webmanifest`, `icons/` | Offline support and install icons for the web app |
| `capacitor.config.json`, `.github/workflows/build.yml` | Android APK build |

The APK signing key is `signing/release.p12`, locked with a long random password. To let GitHub build APKs, add that password as the repository secret `KEYSTORE_PASSWORD` (Settings → Secrets and variables → Actions). Keep the password private and saved somewhere safe — without it, future APKs can't install over the old one.
