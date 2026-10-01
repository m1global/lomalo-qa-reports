# Lomalo QA Reports

Auto-published E2E test-run dashboard for [rmi-wallet](https://github.com/m1global/rmi-wallet)
and [rmi-merchants](https://github.com/m1global/rmi-merchants).

**Nothing under `runs/` or `data/` is edited by hand.** Those are written by
a script (`scripts/publish-qa-report.mjs`, duplicated in both app repos)
running as a step in each repo's `e2e-maestro-smoke-android.yml` CI
workflow, right after the Maestro flows finish. It clones this repo, parses
that run's Maestro JUnit output, appends one entry to `data/index.json`,
writes a **data-only JSON file** under `runs/<repo>/<fileSafeId>.json`
(repo/platform/branch/commit/run metadata + the per-flow pass/fail list),
and pushes straight to `main`. See each app repo's `docs/qa-automation-plan.md`
for the full QA automation plan.

**This repo owns all rendering — the app repos' publisher script does not.**
`index.html` and `detail.html` are the two static, hand-maintained pages:
- `index.html` fetches `data/index.json` at load time and renders the
  filterable runs table.
- `detail.html?run=runs/<repo>/<fileSafeId>.json` fetches that one run's JSON
  file and renders its per-flow table.

Neither page changes per run — only the JSON data they read does. (A small
number of pre-existing `runs/**/*.html` files predate this split, back when
each app repo generated its own detail page HTML; they're left in place
since they still render fine as static pages, but no new ones are written
that way.)

Published via GitHub Pages, deployed by `.github/workflows/deploy-pages.yml`
on every push to `main`.
