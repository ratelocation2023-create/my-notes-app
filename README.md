# Notes — install on your iPhone without the App Store

## Files in your repo

Upload these so they sit at the **top level** of the repo:

```
index.html
manifest.webmanifest
sw.js
icons/
  apple-touch-icon.png
  icon-192.png
  icon-512.png
  maskable-512.png
```

The app is `index.html`, so the site root opens it directly.
If an old `notes.html` is still in the repo, delete it — it is the previous
version and will only confuse you later.

## Install it on the iPhone

1. Open the site in **Safari** (not Chrome, not a browser inside another app).
2. Tap **Share**.
3. Tap **Add to Home Screen**, then **Add**.

Free — no Apple Developer account, no App Store review.

## Every time you change index.html

Phones cache hard. Two steps, every deploy:

1. Open `sw.js` and bump the version: `const CACHE = 'notes-v2';` (then v3, v4 …)
2. Open the installed app once while online. It fetches the new version and
   shows a **Reload** button.

Skip step 1 and the phone keeps showing the old app.

## What works offline

Every note, all six categories, search, calendar, focus timer, drag ordering,
export and import — all of it, once installed.

## About reminders

iOS only allows notifications for a web app added to the Home Screen, never
from a Safari tab. Even then, this app schedules reminders **while it is
open**. If a reminder time passes while the app is closed you get a catch-up
list next time you open it, not a lock-screen alert at that exact minute.

Exact-minute alerts need a push server (VAPID keys plus a backend). Worth
doing only if that precision genuinely matters to you.

## Backups

Everything lives in this browser on this device. It does not sync between your
laptop and your phone, and iOS can clear storage for web apps left unused for
a long time. Use Settings → Export backup now and then, and keep the JSON file
somewhere safe.
