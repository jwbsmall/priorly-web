# priorly-web — Security

Static site, no backend, no auth. Surface area is intentionally tiny — this file documents what little there is and how to report a problem.

## Reporting a vulnerability

Email **josmall@sent.com** with the subject `priorly-web security`. Please don't open a public GitHub issue.

## Trust model

`public/index.html`, `public/invite.html`, and `public/reset.html` are static HTML served by Vercel. They contain no secrets, make no API calls, and accept no user input. The only client-side scripting is one line that copies `window.location.href` into a CTA `<a href>` so the universal-link target opens with the original URL.

`public/.well-known/apple-app-site-association` is a public JSON file — its contents are public by design (Apple fetches it during app installation). It contains the Team ID and bundle ID, both of which are public Apple Developer identifiers.

## Secrets

There are none in this repo. Vercel project tokens (used by the Vercel-GitHub integration) live in the Vercel dashboard, not the repo. There is no Vercel CLI token committed.

If a Vercel access token is ever leaked: revoke it via Vercel → Settings → Tokens → Revoke, then issue a fresh one for the integration.

## Continuous checks

`.github/workflows/secrets-scan.yml` runs gitleaks on every push and PR. If the scan ever flags something, it's a real failure — there are no allowlists in this repo.

## Linked: Priorly iOS

The app side of the same product lives at https://github.com/jwbsmall/Priorly. See its `SECURITY.md` for the full server/auth/RLS picture.
