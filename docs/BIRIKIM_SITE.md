# Birikim Site

## What it is

The public face of Birikim at `birikim.app`: a static site on GitHub Pages with the landing page, the legal texts and
the account deletion page the stores require. It also tells iOS and Android which paths on `birikim.app` belong to
the app, so a link to a record opens it in the app.

## The parts

| Part | What it does | Where | More |
|---|---|---|---|
| Pages | Landing, privacy policy, KVKK, account deletion | `index.html`, `privacy.html`, `kvkk.html`, `delete.html` | [`PAGES.md`](PAGES.md) |
| Legal sources | Privacy policy in Turkish and English, KVKK, Apple's EULA, thanks | `docs/*.md` (privacy and KVKK also as `.docx` and `.pdf`) | [`PAGES.md`](PAGES.md) |
| iOS association | `applinks` and `webcredentials` for `79S2VKLWU7.app.birikim.mobile`; 13 app paths, the site's images excluded | `.well-known/apple-app-site-association` | [`APP_LINKS.md`](APP_LINKS.md) |
| Android association | `app.birikim.mobile` handles all URLs, with three SHA-256 fingerprints | `.well-known/assetlinks.json` | [`APP_LINKS.md`](APP_LINKS.md) |
| Styles and scripts | SCSS and JavaScript sources, the built CSS and JavaScript, images | `src/`, `dist/` | |
| Release note | `changelog/2.0.0_ios.md` | `changelog/` | |

## Publishing

GitHub Pages serves `main` at `birikim.app` (`CNAME`); `_config.yml` includes `.well-known`, which Jekyll would
otherwise skip. There is no build step in the repository: `dist/` is committed as it is served.

## Rules

- A path the app claims is never renamed; the site never uses a claimed path for its own page.
- The privacy policy changes with the app: a new data use is written in both languages before it ships.
- A new signing certificate's fingerprint goes into `assetlinks.json` before a build signed with it ships.

## Decisions

- **A static site.** Nothing to run or patch; the stores' required pages are plain HTML.
- **The app's paths on the site's domain.** A link in a notification or an email works with or without the app.

## Known gaps

- `src/` has no build setup (no package file); `dist/` cannot be rebuilt from it here.
