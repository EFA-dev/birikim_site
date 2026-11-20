# Pages and legal texts

The site's four pages, the legal texts' sources in `docs/`, and where the app reads its own copies.

## The pages

| Page | Language | Last changed | What it says |
|---|---|---|---|
| `index.html` | Turkish | 2024-05-04 | "Birikim - Finans Asistanınız": the App Store and Google Play badges, the eight screenshots of version 2.8 (`dist/webp/v2.8/`), the modules and reports, `info@birikim.app`, Twitter and KVKK links |
| `privacy.html` | English | 2021-11-29 | A privacy policy for a freemium app, effective 2021-11-29: log data, cookies, Google Play Services and Sentry as third parties |
| `kvkk.html` | Turkish | 2024-01-03 | The KVKK notice, word for word `docs/kvkk.md`; contact `info@birikim.app` |
| `delete.html` | Turkish and English | 2026-11-20 | Account deletion as the app does it: Settings › Delete Account, a fresh sign-in, a 7-day wait, taking it back in the app or with the confirmation email's button, what is deleted, and that a subscription is cancelled in the store |

`index.html` loads its animation scripts from unpkg (`animejs@3.0.1`, `scrollreveal@4.0.0`) and its font from Google
Fonts.

## The sources

| File | What it is |
|---|---|
| `docs/privacy_policy.md`, `docs/privacy_policy_en.md` | The privacy policy in Turkish and English (EFA as the Company, the site as the Platform), with the support device log paragraph since 2026-11-11; also as `.docx` and `.pdf` |
| `docs/kvkk.md` | The KVKK notice; also as `.docx` and `.pdf` |
| `docs/apple_eula.md` | Apple's standard licensed application EULA |
| `docs/gratitude.md` | Thanks to the people who helped, in Turkish |

## Where the app reads its texts

The app does not read this site for its legal texts. Its settings `app/terms_url.tr`, `.en` and `app/privacy_url.tr`,
`.en` (`birikim_shared`'s `ConfigCatalog`) point, on dev, at Markdown files under `agreements/` in another Supabase
project's public `public_assets` bucket (`kvkk_tr.md`, `kvkk_en.md`, `privacy_policy_tr.md`, `privacy_policy_en.md`).
Nothing in this repository writes them there.

## The account deletion today

The app deletes an account after a 7-day wait: Settings › Delete account, a fresh sign-in, then the request; the
email that confirms it carries a link that takes it back (`birikim_mobile/docs/SUBSCRIPTION_AND_ACCOUNT.md`).

## Rules

- The privacy policy changes with the app, in both languages, before the change ships.
- The deletion page says what the app does.

## Decisions

- **Sources beside the pages.** The legal texts are kept as Markdown here, so a change shows in a diff.

## Known gaps

- `privacy.html` is the 2021 English text and not `docs/privacy_policy_en.md`: it names no support device log, no EFA ID,
  no push or subscription provider. The site has no Turkish privacy policy page.
- The app's legal texts live in another Supabase project's storage; nothing here publishes `docs/*.md` there, so a change
  to the sources (such as the device log paragraph) reaches the app only by hand.
