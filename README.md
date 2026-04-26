# priorly-web

Static web frontend for [Priorly](https://github.com/jwbsmall/Priorly) (iOS app).

Served at https://priorly.net via Vercel.

## What's here

- `public/index.html` — landing page.
- `public/invite.html` — `/invite/<token>` deep-link target. Universal link opens the iOS app directly; this page is the fallback for desktops or devices without Priorly installed.
- `public/reset.html` — `/reset` deep-link target for Supabase password recovery emails. Same universal-link behavior.
- `public/.well-known/apple-app-site-association` — Apple App Site Association file. Tells iOS that `priorly.net` is owned by the Priorly app (Team ID `763BYZG6SP`, bundle `josmall.BetsWithFriends`). No file extension by design.
- `vercel.json` — sets `Content-Type: application/json` on the AASA path (Vercel needs the override since the file has no extension).

## Deploy

Pushed to GitHub; Vercel auto-deploys from `main`. Custom domain `priorly.net` attached in the Vercel project settings.

## Verify

```sh
curl -I https://priorly.net/.well-known/apple-app-site-association
# Expect: HTTP/2 200, content-type: application/json, no redirects.
```
