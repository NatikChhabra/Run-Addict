# Run Addict

A mobile-first PWA for verified running challenges. Runners sync activities from Strava, join distance / elevation / streak / pace challenges, climb leaderboards and claim rewards; admins publish challenges and ship rewards from a separate console.

**Live:** https://natikchhabra.github.io/Run-Addict/ &nbsp;·&nbsp; **Android:** [`RunAddict-signed.apk`](RunAddict-signed.apk)

## Features

- **Verified activity sync** — Strava OAuth; only `Run`, `TrailRun` and `VirtualRun` activities inside the challenge window count.
- **Anti-cheat review** — suspicious speeds, duplicate activity IDs and weak activity data are routed to admin review instead of the leaderboard.
- **Challenges & events** — distance, elevation (summed `total_elevation_gain`), streak and pace challenges, plus race / club-run registration.
- **Rewards fulfilment** — earned rewards collect delivery details; the admin console builds a shipping packet and tracks the parcel.
- **Installable** — service worker + web manifest for offline shell and home-screen install; signed Android build via Trusted Web Activity.

## Stack

Vanilla HTML / CSS / JavaScript (no build step), service worker, Strava API, Google Identity. Two serverless examples in `api/` show the backend pieces that must not live in the browser (Strava token exchange, admin session gate).

## Project layout

```text
index.html, js/app.js      runner app
admin.html, js/admin.js    admin console
css/styles.css             shared styles
sw.js, manifest.json       PWA shell
api/*.example.js           serverless routes to deploy separately
assetlinks.json            Android TWA domain verification
RunAddict-signed.apk/.aab  signed Android builds
```

## Run locally

```bash
npx serve .
```

Then open `index.html` (runner app) or `admin.html` (admin console).

## Deploying

Strava and Google sign-in both need configuration (client IDs, an exchange endpoint for the Strava secret, authorised origins). Step-by-step notes are in [DEPLOYMENT.md](DEPLOYMENT.md).

> **Note:** the admin console's login is a client-side demo gate, not real authentication. Before running this with real users, put the admin route behind a server-side session — `api/admin-auth.example.js` is a starting point.

## Installing on a phone

- **Android:** install the APK above, or open the live URL in Chrome → *Install app*.
- **iPhone:** open the live URL in Safari → Share → *Add to Home Screen*.
