# Notes — installing on iPhone without the App Store

## What you upload

Keep this exact folder structure in your GitHub Pages repo:

```
notes.html
manifest.webmanifest
sw.js
icons/
  apple-touch-icon.png
  icon-192.png
  icon-512.png
  maskable-512.png
```

All five paths are relative, so it works whether you serve from the repo root
or a subfolder — as long as the files stay together.

## Installing it on the iPhone

1. Open the page in **Safari** (not Chrome, not an in-app browser).
2. Tap the **Share** button.
3. Tap **Add to Home Screen**, then **Add**.

You now have a Notes icon on the home screen. It opens full screen with no
address bar. This is free — no Apple Developer account, no App Store review.

## After you change notes.html

Phones cache aggressively. Two steps every time you deploy:

1. Bump the version in `sw.js`: `const CACHE = 'notes-v2';` (then v3, v4 …)
2. Open the installed app once while online. It downloads the new version and
   offers a **Reload** button.

If you skip step 1 the phone may keep serving the old file.

## What works, and what does not

Works offline once installed: every note, all six categories, search,
calendar, focus timer, drag ordering, export and import.

Reminders: iOS only allows notifications for a web app that has been added to
the home screen — never from a Safari tab. Even then, this app schedules
reminders **while it is open**. If a reminder time passes while the app is
closed, you get a catch-up list the next time you open it, not a lock-screen
alert at the exact minute.

For alerts that arrive when the app is closed you need a push server (VAPID
keys plus a backend to send them). That is a bigger change and is worth doing
only if the exact-minute alert really matters to you.

## Storage

Everything lives in this browser's storage on this device. It does not sync
between your laptop and your phone. iOS can also evict storage for web apps
left unused for a long stretch, so use Settings → Export backup from time to
time and keep the JSON file somewhere safe.
