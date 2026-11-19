# birikim_site

Birikim's website at `birikim.app`, served by GitHub Pages: the landing page, the privacy policy, the KVKK notice, the
account deletion page the stores ask for, the legal texts' sources, and the two files that claim the app's paths for
universal links.

## What it holds

| Part | What it does |
|---|---|
| `index.html` | The landing page: the App Store and Google Play badges, the app's eight screenshots (`dist/webp/v2.8/`), the modules, contact and KVKK links |
| `privacy.html` | A privacy policy in English, effective 2021-11-29 |
| `kvkk.html` | The KVKK notice in Turkish, the same text as `docs/kvkk.md` |
| `delete.html` | How to delete a Birikim account, in Turkish |
| `.well-known/apple-app-site-association` | Claims the app's 13 paths (`/incomes`, `/bills/*` … `/inbox/*`) for iOS; the site's images and icons excluded |
| `.well-known/assetlinks.json` | Lets the Android app (`app.birikim.mobile`) handle all URLs, with its three signing certificates' fingerprints |
| `docs/` | The legal texts' sources: privacy policy (Turkish, English), KVKK, Apple's EULA, thanks |
| `src/`, `dist/` | The styles (SCSS) and scripts, the built CSS and JavaScript, images |
| `changelog/` | One release note |

## Use

A link such as `https://birikim.app/bills/8f2c` opens the bill in the app when it is installed (the path is one of
`birikim_shared`'s `AppPathManager`), and this site otherwise.

## Stands on, used by

- **Stands on:** GitHub Pages (`CNAME`, `_config.yml` keeps `.well-known`).
- **Used by:** Birikim's users, the App Store and Google Play (privacy and deletion pages), iOS and Android (app links),
  `birikim_mobile`'s link test (reads the iOS file beside the app).

## Run

Pushing to `main` publishes the site. A local look:

```bash
python3 -m http.server 8000
```

## More

- [`docs/BIRIKIM_SITE.md`](docs/BIRIKIM_SITE.md): the parts, publishing, rules, decisions and known gaps.
- [`docs/APP_LINKS.md`](docs/APP_LINKS.md): how the app's paths are claimed and kept in step.
- [`docs/PAGES.md`](docs/PAGES.md): the pages and the legal texts, and where the app reads its own.
- [`.agents/skills/birikim-site/SKILL.md`](.agents/skills/birikim-site/SKILL.md): the agent's guide (rules, parts, pitfalls).
