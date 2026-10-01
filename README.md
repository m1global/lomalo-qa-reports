# Lomalo QA Reports

Auto-published E2E test-run dashboard for [rmi-wallet](https://github.com/m1global/rmi-wallet)
and [rmi-merchants](https://github.com/m1global/rmi-merchants).

**Nothing in this repo is edited by hand.** Every file under `runs/` and
`data/index.json` is written by a script (`scripts/publish-qa-report.mjs`,
duplicated in both app repos) running as a step in each repo's
`e2e-maestro-smoke-android.yml` CI workflow, right after the Maestro flows
finish. It clones this repo, parses that run's Maestro JUnit output, appends
one entry to `data/index.json`, writes a detail page under `runs/<repo>/`,
and pushes straight to `main`. See each app repo's
`docs/qa-automation-plan.md` for the full QA automation plan.

`index.html` is the one static, hand-maintained page: a dashboard that
fetches `data/index.json` at load time and renders it. It never changes
per run.

Published via GitHub Pages, deployed by `.github/workflows/deploy-pages.yml`
on every push to `main`.
