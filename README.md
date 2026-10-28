# Second Brain 🧠

A personal second-brain app: notes, tasks with due dates, daily journal, tags, linked notes, photos and files, plus a Discover tab with weather, currency, news and Wikipedia search, and a file converter for photos, PDFs, video, music, Word and Excel files. Works offline, syncs to the cloud when you sign in, and backs up daily.

## Install

- **Android app:** download [second-brain.apk](https://github.com/khalil203/second-brain/raw/main/dist/second-brain.apk) and open it (allow "Install unknown apps" for your browser when asked).
- **Web app:** open https://khalil203.github.io/second-brain/ in Chrome, then menu ⋮ → **Install app**.

## Converter

The Convert tool (Home → Convert, or Discover) changes files on the device: images (JPG, PNG, WEBP, PDF), PDF (JPG, PNG, TXT), video and audio via ffmpeg.wasm (MP4, MP3, GIF, WEBM, M4A, WAV, OGG), spreadsheets via SheetJS, Word via mammoth. The donut format picker is inspired by [Filee](https://github.com/KnifeLemon/Filee) (MIT, © Myeonggu Kim). The desktop version is [Second Brain Convert](https://github.com/khalil203/second-brain-convert).

## Cloud

Sign-in, sync and daily backups use a Supabase project (`kshhznqxudcaipizpxvv`, Singapore). Each account can only read its own notes and files (row-level security). The `web` edge function powers link previews and news feeds.

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
