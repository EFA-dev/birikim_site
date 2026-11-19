---
name: birikim-site
description: Use birikim_site as Birikim's static website at birikim.app on GitHub Pages (landing page, privacy policy, KVKK notice, account deletion page, the legal texts' sources and the app's universal link files). Apply when changing a page or a legal text, claiming or checking an app path, adding a signing certificate's fingerprint, or explaining what the site serves.
kind: project
visibility: internal
repo: birikim_site
---

# Birikim Site

`birikim_site` is Birikim's public face at `birikim.app`: a static site served by GitHub Pages, with the landing
page, the privacy policy, the KVKK notice and the account deletion page the stores ask for, the legal texts' sources
in `docs/`, and the two files that tell iOS and Android which paths on `birikim.app` belong to the app. The paths are
`birikim_shared`'s `AppPathManager`; `birikim_mobile`'s link test reads the iOS file from beside the app. It has no
build step, no config and no server: what is committed is what is served. The app does not read its legal texts from
here.

## Rules

- A path the app claims is never renamed; the site never serves a page of its own on a claimed path.
- A new signing certificate's fingerprint goes into `.well-known/assetlinks.json` before a build signed with it ships.
- The privacy policy changes with the app: a new data use is written in Turkish and English before it ships.
- The deletion page says what the app does.
- `_config.yml` keeps `include: [".well-known"]`; without it Jekyll skips the association files.

## Overview

| Part | What it does |
|---|---|
| `index.html` | The Turkish landing page: store badges, the eight screenshots of version 2.8 (`dist/webp/v2.8/`), the modules, contact and KVKK links |
| `privacy.html` | The 2021 English privacy policy |
| `kvkk.html` | The KVKK notice, word for word `docs/kvkk.md` |
| `delete.html` | How to delete a Birikim account, in Turkish |
| `.well-known/apple-app-site-association` | `applinks` and `webcredentials` for `79S2VKLWU7.app.birikim.mobile`: the 13 app paths, each with its `/*`, after two exclusions for the site's images (`/assets/*.*`, `/assets/svg/*`) |
| `.well-known/assetlinks.json` | `app.birikim.mobile` handles all URLs, with three SHA-256 certificate fingerprints |
| `docs/privacy_policy.md`, `privacy_policy_en.md`, `kvkk.md`, `apple_eula.md`, `gratitude.md` | The legal texts' sources (privacy and KVKK also as `.docx` and `.pdf`) |
| `src/`, `dist/` | SCSS and JavaScript sources; the built CSS, JavaScript and images, committed as served |
| `CNAME`, `_config.yml` | The domain and what Jekyll includes |

## Choosing

- A new app path → `AppPathManager` in `birikim_shared` first, then both association files here and the app's
  entitlements and Android manifest filter, in step.
- A legal text change → its Markdown source in `docs/` (both languages), then the page that shows it and its
  `.docx`/`.pdf`; the app's own copies (the `app/terms_url.*` and `app/privacy_url.*` settings) are elsewhere.
- A style or script → edit `src/` and `dist/` together; nothing here rebuilds `dist/`.

## Workflow

1. Read `docs/BIRIKIM_SITE.md` and, for links, `docs/APP_LINKS.md`; for pages and legal texts, `docs/PAGES.md`.
2. Change the page or file; check JSON files parse (`python3 -m json.tool .well-known/assetlinks.json`).
3. After a change to the claimed paths, run `birikim_mobile`'s link test with this repository checked out beside it.
4. Look at it locally, then update the document that names the part in the same commit.

## Run

- **Config:** none; no `config/<env>.env`.
- **Branch:** work is committed on `dev`; GitHub Pages serves `main` at `birikim.app`, so nothing goes to `main`
  until the owner says so (rule 36).

```bash
python3 -m http.server 8000
cd ../birikim_mobile && flutter test test/managers/app_link_manager_test.dart
```

## Pitfalls

- Renaming or dropping a claimed path: links in sent notifications and emails stop opening the app. Keep the old one.
- A site page or image under a claimed path: iOS hands it to the app. Images go under `/assets/` with a dot in the
  name, icons under `/assets/svg/`.
- Removing `.well-known` from `_config.yml`: the association files are no longer served.
- Editing only `src/`: the site serves `dist/`.
- Expecting the app to show a changed `docs/*.md`: the app reads its texts from storage that nothing here writes.

## References

- `docs/BIRIKIM_SITE.md`: parts, publishing, rules, decisions, known gaps.
- `docs/APP_LINKS.md`: the claimed paths, iOS and Android, how they are kept in step.
- `docs/PAGES.md`: the pages, the legal texts, where the app reads its own.
- `birikim_shared` (`AppPathManager`) and `birikim_mobile`'s `docs/LINKS_AND_NOTIFICATIONS.md`.
- efa_mcp: `check_efa_skills`.
