# Sally App Shell

A lightweight Capacitor project whose only job is to load the live Sally
website inside a real native Android app — using its own private WebView,
not Chrome. No browser bar, no app-lock conflicts, no Chrome dependency.

Live site loaded by the app:
https://mraayanshaikh37.github.io/sally-roleplay-ai/

The app is just a shell. Sally's actual chatbot logic, personality, and API
calls live on that site. Any update pushed there shows up in the app
instantly, with no need to rebuild the APK.

## What's in this repo

- `capacitor.config.json` — app identity (name, ID), the live URL to load,
  and splash screen settings
- `package.json` — Capacitor dependencies (versions already fixed —
  `@capacitor/splash-screen` must be `^6.0.0`, not `^6.1.2`, which doesn't
  exist on npm)
- `index.html` / `www/` — placeholder only, never actually shown (the app
  loads the live URL instead)
- `.github/workflows/build.yml` — GitHub Actions workflow that builds the
  APK automatically on every push

## Icon and splash screen (optional, add later)

This starter repo ships with Android's default icon and splash screen.
To customize them, same pattern as the Sakhi app shell:

1. Create `custom-icons/mipmap-mdpi/`, `mipmap-hdpi/`, `mipmap-xhdpi/`,
   `mipmap-xxhdpi/` — each containing `ic_launcher.png`,
   `ic_launcher_round.png`, `ic_launcher_foreground.png`
2. Create `custom-splash/` with flat-named PNGs:
   `drawable-port-mdpi.png`, `drawable-port-hdpi.png`,
   `drawable-port-xhdpi.png`, `drawable-port-xxhdpi.png`,
   `drawable-land-mdpi.png`, `drawable-land-hdpi.png`,
   `drawable-land-xhdpi.png`, `drawable-land-xxhdpi.png`

The workflow checks for these folders automatically — if they don't exist,
it just skips that step and uses the defaults. No workflow edits needed to
add them later; just create the folders and push.

## How to get the APK

1. Go to the **Actions** tab of this repo
2. Open the most recent successful "Build Android APK" run (green check)
3. Scroll to **Artifacts**, download `sally-app-debug`
4. Unzip it, install `app-debug.apk` on your phone
   (allow "install from unknown sources" if prompted)

## Making changes

**Change the app name, live URL, or splash timing:**
Edit `capacitor.config.json`, commit — the Action rebuilds automatically.

**Change what Sally says or how she behaves:**
That's not in this repo — edit Sally's actual site
(mraayanshaikh37.github.io/sally/ repo), not here.

## Notes carried over from building the Sakhi app shell

- This is a debug build (unsigned) — fine for personal use, not the Play
  Store.
- `android/` is intentionally in `.gitignore` — it's fully regenerated on
  every build by `cap add android`, so files placed there directly would be
  wiped out. Custom icons/splash live in `custom-icons/` and
  `custom-splash/` and get copied into place by the workflow instead.
- GitHub's mobile upload can't create nested folders or take a custom
  upload path — create each new folder first via "Create new file" with the
  full path typed out, then upload into it.
- Editing JSON files through GitHub's mobile web editor can occasionally
  introduce invisible characters that silently break parsing. If a config
  file starts failing for no visible reason, delete and recreate it fresh.
- Every build takes ~1.5–2 minutes regardless of how small the change is.
