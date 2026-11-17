# App links

A path on `birikim.app` that names one of the app's screens is claimed by the app: with the app installed, a tap on
`https://birikim.app/bills/8f2c` opens the bill there; without it, the browser opens this site. The paths are
`birikim_shared`'s `AppPathManager`: record ids only, never renamed.

## The claimed paths

| Path | Screen |
|---|---|
| `/incomes`, `/expenses`, `/bills`, `/vehicles`, `/subscriptions`, `/goals`, `/assets`, `/debts`, `/habits`, `/budgets`, `/tasks`, `/shopping` | A module's section; with `/*`, a card or an item |
| `/inbox`, `/inbox/*` | The inbox and a notification's detail |

## iOS

`.well-known/apple-app-site-association`:

- `applinks` for `79S2VKLWU7.app.birikim.mobile`, one component for each path and one for its `/*`.
- Two exclusions first: `/assets/*.*` (the site's images: an app path never carries a dot) and `/assets/svg/*` (the
  site's icons). `/assets` is also the asset module's path.
- `webcredentials` for the same app id.

The app's entitlements hold `applinks:birikim.app` and `webcredentials:birikim.app`.

## Android

`.well-known/assetlinks.json` grants `delegate_permission/common.handle_all_urls` to `app.birikim.mobile` with three
SHA-256 certificate fingerprints. Which paths the app takes is in its manifest: an https filter for `birikim.app` with
the same 13 path prefixes.

## Kept in step

`birikim_mobile/test/managers/app_link_manager_test.dart` reads this repository's iOS file from beside the app
(`../birikim_site/`), and checks that its claimed paths, the Android filter and `AppPathManager`'s sections are the
same set. It skips when `birikim_site` is not checked out there. `assetlinks.json`'s fingerprints are not tested.

## Rules

- A claimed path is never renamed; a moved screen keeps its old path in the app as an alias.
- The site never serves a page on a claimed path.
- A new signing certificate's fingerprint goes into `assetlinks.json` before a build signed with it ships.

## Decisions

- **Only the app's paths.** The domain stays the site's for everything else, so the landing and legal pages open in a
  browser even with the app installed.

## Known gaps

- None recorded.
