# GSA/sam-design-system context
> refreshed 2026-09-05 | upstream default: master @ 3cef125c3e4d98debf5aba1890b9bd6830725e4e

## Identity & policies
- upstream: GSA/sam-design-system, default branch `master`, primary language TypeScript (Angular 17 Nx monorepo), English-first (yes — issues/UI/docs all English).
- CLA/DCO: none (no CLA bot, no DCO requirement found in CONTRIBUTING).
- AI-assisted PR policy: unstated (no AI/LLM/generated/ChatGPT/Copilot mention in CONTRIBUTING.md, README, or PR template; no GSA/.github org repo exists).
- signed commits required: no (no branch-protection signature requirement).
- PR template: `.github/PULL_REQUEST_TEMPLATE.md` (JIRA ticket in title, imperative mood, Type of Change checkboxes, browser-test checkboxes, checklist).
- external tracker: GitHub issues + JIRA ticket numbers referenced in PR titles (e.g. IAEMOD-47404, IAE-500). No external tracker pointer in CONTRIBUTING.
- org defaults: none (GSA/.github repo does not exist; repo's own CONTRIBUTING governs).

## Conventions (verified from merged PRs)
- branch naming: mixed. Issue-number-prefixed kebab (`1515-fix-add-validation`, `1535-modulardashboard-blur-validation`, `1529-add-toggle-to-grey-out-disable-panel-in-side-navigation-component`) and JIRA-prefixed (`IAEMOD-47404`) both common. For issue-driven work use `<issue-number>-<kebab-description>`.
- commit style: plain imperative, no Conventional Commits prefix observed in recent history.
- test command: `npm run test:components` / `test:material-extensions` / `test:sam-formly` (Karma/Jasmine, ChromeHeadlessCI). `npm test` runs all three.
- lint: `npm run lint` (`ng lint`). prettier: `npm run test:prettier`.
- CI that gates merge: CircleCI (`.circleci/config.yml`) runs prettier + all three test suites + publish dry-run. GitHub Actions only build/deploy Storybook (no tests/lint). CircleCI is NOT connected to Oli's fork — fork PRs show no green substantive check; local verification required.
- how outside PRs get merged: slow. master last commit 2025-01-31; most recent merged PR #1593 (2025-09-04) targeted `ng-18` branch, not master. External merge rate low; maintainers are mid Angular-18 upgrade on `ng-18`.

## Maintainer picture
- active maintainers: cwolf10 (stepper/autocomplete/tabs/table), yerramshilpa (stepper, filters, Angular upgrades), shayan-roshan (filters), addiedavis, davereed, Nysharma, brandydanner-gsa.
- in-flight maintainer work (avoid duplicating): Angular 18 upgrade (`ng-18` branch, PRs #1596/#1597), stepper blur validation (#1535, #1586), horizontal filter reset (#1495, PR #1563), rowClick emit (#1276, PR #1278), tabs styling (#1468).
- response latency: issues get maintainer comments but fixes are slow to land on master; repo effectively dormant on master since Jan 2025.

## Issue-area health
- stepper: contested/active (multiple open issues #1515, #1535, #1586, #1585; maintainer PRs merged #1572/#1573). Avoid — maintainer-claimed.
- autocomplete: #1448 (Enter key selects first option instead of hovered) — cwolf10 confirmed repro, unassigned, open since 2024-04. Good candidate.
- external-link: #1063 (innerHTML hyperlinks) — assigned to davereed (maintainer). Avoid.
- accordion: #1014 (UsaAccordionHeader 508) — unassigned, addiedavis says persists. Candidate.
- filters: #1495/#1506/#1080 — maintainer-claimed or contested. Avoid.
- a11y/508: many open (#1591, #1589, #1446, #1056, #1054, #1053) — mostly unassigned, but 508 fixes need JAWS/AMP verification we cannot run. Lower priority.

## Gap ledger (dedupe — READ FIRST, never re-pick)
- (no prior runs in this repo yet — first contribution cycle)

## Mined gaps (discovered, not yet attempted)
- 2026-09-05 autocomplete-search: no `(mouseover)` handler on result list items, so hovering an option does not update `highlightedItem`/`highlightedIndex`; pressing Enter after hovering a non-first option selects the FIRST option instead of the hovered one (issue #1448, cwolf10 confirmed repro). Repro: open autocomplete, mouse over option index 2, press Enter -> results[0] selected. Dedupe: no open/merged PR covers this (PR #1572/#1550 are stepper, unrelated). Proposed test: open autocomplete, call onItemHover(results[2]), press Enter, assert results[2] selected. Status: proposed.
