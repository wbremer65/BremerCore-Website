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
  `https://duplicateandphoto-agent.onrender.com`. *(edited 2026-08-12, not
  yet committed/pushed — see below)*
- [ ] In the GitHub repo (`wbremer65/BremerCore-Website`) → **Settings →
  Pages**:
  - Source: "Deploy from a branch" → `main` / `(root)`.
  - Confirm the custom domain field shows `bremercore.com` (should
    auto-populate from the committed `CNAME` file — verify it actually did).
- [ ] Once DNS has propagated and GitHub finishes issuing the certificate,
  enable **"Enforce HTTPS"** in that same Pages settings page. No need to
  buy an SSL certificate — GitHub Pages issues one automatically via Let's
  Encrypt once the custom domain is verified.
- [ ] Before pointing Lemon Squeezy's store review at the live site,
  confirm the two placeholders flagged inline on the legal pages are
  finalized:
  - 14-day refund window (`refund.html`)
  - Governing-law jurisdiction, currently South Africa (`terms.html`)
- [ ] Visit `https://bremercore.com` and `https://www.bremercore.com` once
  HTTPS is enforced — confirm both load, and that the suggestion form on
  `filetwin.html`/`photochecker.html` submits successfully against the
  live API (not a CORS/404 error from a stale `localhost` URL).
