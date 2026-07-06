# RNG OPS TIMER

A single-file, offline **random mystery timer** with a military-fitness style UI.

You set a **min–max time range** (hours, minutes + seconds). The app secretly picks a
random duration inside that window — down to the exact second, so it won't just land on
a round minute — and you're **not** told the number. You hit **START**, the
countdown runs **hidden** (no numbers, just a radar/status display), and when it hits
zero an **alarm sounds**, the screen shows **FINISHED**, and only then is the sealed
duration revealed.

Great for interval training, unpredictable holds/rests, or any drill where you
shouldn't be able to pace yourself against the clock.

## How to use it on your phone (no hosting, no install)

Everything lives in **`index.html`** — one file, 100% offline, no server or internet.

1. Get `index.html` onto your phone. Any of these work:
   - Email/AirDrop/message the file to yourself and open it.
   - Save it to Files / Google Drive / your phone's storage and tap it.
2. It opens in your mobile browser (Safari / Chrome) and runs immediately.
3. **Optional — make it feel like a real app:** with the page open, use the browser
   menu → **Add to Home Screen**. You'll get an app icon that launches full-screen
   with no address bar.

> First time you press a button, that tap "unlocks" audio (a mobile browser rule),
> so the alarm is guaranteed to fire later. Keep the screen on during a run — the app
> requests a wake lock where supported.

## Flow

1. **SET TIME RANGE** — dial in MIN (lower bound) and MAX (upper bound) as HH:MM:SS.
2. **LOCK RANGE** — a random duration is sealed (chosen to the second, inclusive of
   both bounds). It is never displayed.
3. **START TIMER** — countdown begins, fully hidden.
4. **At zero** — loud repeating alarm tone, red flash, **FINISHED**, and the sealed
   duration is revealed. **DISMISS ALARM** to silence, **NEW MISSION** to reset.

You can **ABORT MISSION** any time during a run to bail back to setup.

## Notes

- **Remembers your range:** the last min/max you set is saved on the device, so
  reopening the app restores your values instead of the defaults.
- **Alarm:** a synthesized two-tone beep generated in-browser (Web Audio) — no audio
  file needed, works fully offline. It loops until you dismiss it.
- **Rings even when the phone is locked / app is backgrounded:** iOS freezes a web
  app's code the moment you leave it, so a plain countdown can't ring in the
  background. Workaround: when you press START the app immediately begins playing a
  single silent audio track with the alarm tone baked onto the end of it. Audio that's
  already playing keeps playing through a screen-lock, so the alarm still sounds at
  zero. This is the best a home-screen web app can do — a native app is the only way to
  *guarantee* background alarms. Pre-rendered for durations up to 1 hour; longer timers
  fall back to ringing when you reopen the app. The screen is also kept awake (Wake
  Lock) while a timer runs and the app is open.
- **Accuracy:** the countdown is based on a wall-clock deadline, so it stays correct
  even if the browser throttles the tab in the background; it fires promptly when you
  return to the app.
- **Home-screen icon:** ships a custom tactical "mystery stopwatch" icon
  (`apple-touch-icon.png` / `icon-*.png`) and a web app manifest, so **Add to Home
  Screen** gives a proper app icon and a full-screen standalone launch.
- **Range:** hours 0–23, minutes 0–59, seconds 0–59. MAX must be ≥ MIN and above
  00:00:00.
