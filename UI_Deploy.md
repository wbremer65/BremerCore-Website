# BremerCore-Website — GitHub Pages Deploy

Deploy checklist for publishing `bremercore.com` via GitHub Pages.

**The desktop `.exe` build does *not* belong in this file** — it lives in
`API_Deploy.md` (in `DuplicateAndPhoto-Agent/license_backend/`), since
rebuilding it is only about pointing the desktop client at the live API
URL, and has nothing to do with this website or its repo.

Do the API deploy first if you haven't — one step below needs its live URL.

## Steps

- [x] Merge `develop` → `main` and push. *(Done 2026-08-05 — `main`
  previously only had the initial commit; the real pages are now on `main`.)*
- [x] DNS at frikkadel.co.za: 4 GitHub Pages A records at the apex
  (`185.199.108.153` / `.109.153` / `.110.153` / `.111.153`) + `www` CNAME
  → `wbremer65.github.io`. *(Done 2026-08-06.)*
- [x] `mail.bremercore.com` A record + MX fix + cPanel Email Forwarder for
  `werner@bremercore.com`, confirmed working with a test email. *(Done
  2026-08-06 — needed for the Lemon Squeezy signup in `API_Deploy.md`, not
  for the website itself, but handled in the same DNS session.)*
- [x] Update `API_BASE_URL` in `filetwin.html` and `photochecker.html`
  (used by the suggestion-form `fetch()` calls) to the live API URL,
  `https://duplicateandphoto-agent.onrender.com`. *(done 2026-08-12,
  committed `abb55ca`, pushed — confirmed live on the real site.)*
- [x] In the GitHub repo (`wbremer65/BremerCore-Website`) → **Settings →
  Pages**: Source = "Deploy from a branch" → `main` / `(root)`, custom
  domain = `bremercore.com`. *(done 2026-08-12 — this was the missing
  piece; DNS alone doesn't register the domain with GitHub Pages, it had
  to be set/saved explicitly here too.)*
- [x] Enabled **"Enforce HTTPS"**. *(done 2026-08-12.)* Confirmed live:
  `http://bremercore.com` → `301` redirect to HTTPS, `https://bremercore.com`
  → `200` with a valid auto-issued Let's Encrypt cert. No certificate
  purchase was needed anywhere in this stack.
  - `https://www.bremercore.com` not resolving yet as of 2026-08-12 —
    apex cert issued fine, `www` variant's cert appears to still be
    provisioning on GitHub's side. Recheck later rather than re-touch any
    settings; nothing on our end looks misconfigured.
- [x] 14-day refund window confirmed (`refund.html`) — placeholder
  callout removed. *(done 2026-08-12)*
- [ ] Governing-law jurisdiction, currently South Africa (`terms.html`)
  — still needs Werner's confirmation with his accountant/legal advisor,
  same open item as the VAT question.
- [x] **Bonus fix while checking this**: `hello@bremercore.com` (used
  13 times across 6 pages) was never actually live — set up `refund@`
  and `support@` as real forwarders instead (removed the unused `admin@`
  too, since it's a common spam target). Updated every page: refund-page
  contact links → `refund@bremercore.com`, everything else (privacy/terms
  questions, launch notifications, footers) → `support@bremercore.com`.
  *(done 2026-08-12)*
- [x] Confirmed the live site actually serves the updated code: fetched
  `https://bremercore.com/filetwin.html` and verified `API_BASE_URL`
  matches the deployed API, not a stale `localhost` value. *(done
  2026-08-12)* Re-check `www.bremercore.com` once its cert is ready.
