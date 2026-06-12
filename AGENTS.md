<!-- comm-contract:start -->

## Communication Contract

- Inherit global Codex communication and reporting rules from `/Users/d/.codex/AGENTS.override.md` and `/Users/d/.codex/policies/communication/BigPictureReportingV1.md`.
- Repo-specific instructions below add project constraints only; do not restate global voice or status-reporting rules here.
<!-- comm-contract:end -->

## Inherited Operating Rules

- Inherit global git, review/fix, testing, docs, skill-use, and reporting gates from `/Users/d/.codex/AGENTS.md` and active session instructions.
- Use `.codex/verify.commands` and `.codex/scripts/run_verify_commands.sh` as this repo-local verification authority when present.
- Keep the project-specific portfolio constraints below as the source of truth for runtime, privacy, and release risks.

<!-- portfolio-context:start -->

# Portfolio Context

## What This Project Is

TicketDash is a native desktop dashboard for assigned Jira tickets. It syncs tickets locally, calculates business-hours SLA metrics, shows charts for workload trends, categorizes work, and keeps Jira data searchable without needing the browser.

## Current State

The repo is active IT workflow tooling. Existing local changes are PR-template metadata plus an untracked lockfile, so context recovery should remain documentation-only.

## Stack

| Layer         | Technology                                                   |
| ------------- | ------------------------------------------------------------ |
| Desktop shell | Tauri 2                                                      |
| Frontend      | React, TypeScript, Tailwind CSS                              |
| Charts        | Recharts                                                     |
| Backend       | Rust — Jira sync, business-hours calculation, categorization |
| Storage       | SQLite (local app data dir)                                  |

## How To Run

```bash
# Start in development mode
npm run tauri dev
```

Configure your Jira URL and API token in **Settings** on first launch.

## Known Risks

- Jira API tokens are sensitive and should stay in app settings/local storage, not source.
- Business-hours metric calculations live in Rust and should remain deterministic.
- The frontend should read from the local cache; network calls belong in sync paths.
- Keep PR-template and lockfile drift separate from Jira sync or metrics changes.

## Next Recommended Move

Resolve PR-template and lockfile drift separately, then verify Jira sync, local cache search, business-hours metrics, charts, and background refresh before shipping changes.

<!-- portfolio-context:end -->
