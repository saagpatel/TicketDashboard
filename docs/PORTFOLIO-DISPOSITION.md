# TicketDashboard (TicketDash) — Portfolio Disposition

**Status:** Release Frozen — Tauri 2 + Rust + React Jira ticket
dashboard on `origin/main` with explicit Phase 3 delivery
(`PHASE3_PLAN.md` + `PHASE3_STATUS.md` on canonical main) covering
background scheduler and sync progress events. Joins the signing
cluster as the 15th member.

> Disposition uses strict `origin/main` verification.

---

## Verification posture

This repo has only `origin` (`saagpatel/TicketDashboard`) — **no
`legacy-origin` remote**. The legacy-origin trap from
FreeLanceInvoice / PersonalKBDrafter / BattleGrid / PomGambler /
LegalDocsReview does not apply here.

But this repo has a different twist: **no local `main` branch
exists**. The clone has `master` (no upstream, unmerged), plus a
handful of `codex/*` bootstrap branches. The current HEAD before
this disposition pass was `codex/chore/bootstrap-codex-os`, which
sits behind canonical `origin/main`. Reactivation must start from
`origin/main`, not from any local branch.

Specifically verified on `origin/main`:

- Tip: `b503ea9` chore: add pull request template
- Substantive commits on `origin/main`:
  - `5767eee` chore(repo): finalize codex os bootstrap baseline
  - `dce0c4e` feat(dev): add lean dev mode and cleanup scripts
  - `0283dd4` fix(security): harden release gates and sync correctness
  - `3f0fc2f` docs: comprehensive README with features, setup, and usage guide
  - `ae0b196` feat: initial commit with security and stability fixes
- Phase docs present on `origin/main`:
  - `PHASE3_PLAN.md`
  - `PHASE3_STATUS.md` (Step 25: Background Scheduler ✅, Step 26:
    Sync Progress Events ✅ visible from the rendered headings)
- Tree on `origin/main` is a real Tauri 2 desktop app with Jira
  integration:
  - `src-tauri/src/commands/{tickets,sync,settings,mod}.rs`
  - `src-tauri/src/db/{migrations,queries,mod}.rs`
  - `src-tauri/src/jira/client.rs`
  - `src-tauri/src/errors.rs`
- Release scaffolding: none yet (no `RELEASE-READINESS.md`,
  no `release-smoke.yml`)
- Default branch: `main`

---

## Why "Release Frozen" instead of other dispositions

- **Active** — wrong. Phase 3 (background scheduler, sync progress
  events) is explicitly closed out in `PHASE3_STATUS.md` on
  canonical main. The product surface is complete; only signing is
  missing.
- **Cold Storage / Archived** — wrong. Recent security/release-gate
  fix commits (`0283dd4 fix(security): harden release gates and
sync correctness`) show active hardening.
- **Release Frozen** — correct. Joins the cluster.

This is the **15th signing cluster member**: DesktopPEt / ContentEngine
/ AIGCCore / Relay / FreeLanceInvoice / Nexus / DeepTank / OPscinema /
ShipKit / SignalFlow / PixelForge / DatabaseSchema / LegalDocsReview /
WorkdayDebrief / **TicketDashboard**.

---

## Current state in one paragraph

TicketDash is a Tauri 2 + Rust + React Jira ticket dashboard for
team-lead and personal-productivity use cases (per the on-origin/main
README). Backend: src-tauri with `jira/client.rs`, command modules
for tickets / sync / settings, SQLite (migrations + queries module),
typed error layer. Phase 3 explicitly delivered: background
scheduler for periodic sync and sync-progress events surface to
frontend. The README markets daily standups, SLA compliance, focused
workflow, and team-leads/managers as use cases.

For full detail see:

- `README.md` on `origin/main`
- `PHASE3_PLAN.md`
- `PHASE3_STATUS.md`

---

## Unblock trigger (operator)

When ready to ship:

1. Wire Apple Developer ID + notarization credentials.
2. Decide Jira credentials posture for v1 distribution:
   - Per-user OAuth (each user authorizes their own Jira instance)
   - API token + URL (operator-supplied per install)
   - Hybrid
     Cleanest fit for a multi-tenant desktop app is OAuth, but the
     current `jira/client.rs` should be audited before signing to
     confirm it doesn't bake in a development OAuth client ID.
3. Cut v1.0.0 release tag (Phase 3 closed out — natural rev).
4. Verify signed/notarized DMG opens cleanly with no Gatekeeper
   warnings.

Estimated operator time once credentials are in hand: ~3 hours
including Jira credential audit and notarization round-trip.

---

## Portfolio operating system instructions

| Aspect               | Posture                                                                                                                                                                                                                                           |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Portfolio status     | `Release Frozen`                                                                                                                                                                                                                                  |
| Review cadence       | Suspend overdue counting                                                                                                                                                                                                                          |
| Resurface conditions | (a) Apple signing credentials wired, (b) operator picks Jira credential distribution model, or (c) operator opens a Phase 4 scope packet                                                                                                          |
| Co-batch with        | Signing cluster: DesktopPEt / ContentEngine / AIGCCore / Relay / FreeLanceInvoice / Nexus / DeepTank / OPscinema / ShipKit / SignalFlow / PixelForge / DatabaseSchema / LegalDocsReview / WorkdayDebrief / **TicketDashboard** — **now 15 repos** |
| Special concern      | **Local missing `main` branch.** Reactivation must explicitly fetch and check out `origin/main`.                                                                                                                                                  |
| Special concern      | **Jira credential model** must be settled before public distribution — affects user onboarding flow.                                                                                                                                              |

---

## Why this row has a "no local main" quirk

Most repos this session had a local `main` branch (possibly
mistracking `legacy-origin/main`). TicketDashboard has no local
`main` at all — only `master` (no upstream) and `codex/*` bootstrap
branches. The remote `origin` has `main` as default. So the
reactivation procedure has one extra step: explicitly create the
local `main` branch from `origin/main` before any work.

This is a new quirk for the session — distinct from the
legacy-origin trap (where local main exists but mistracks) and the
branch trap (where local main exists but lags). Worth flagging in
case other repos share this shape.

---

## Reactivation procedure (for the next code session)

1. **Create local `main` from `origin/main`:**
   ```bash
   git fetch origin
   git checkout -b main origin/main
   ```
2. Review the local stash (`r8-ticketdashboard-stash`) — contains
   modifications to package.json, perf scripts, `src-tauri/src/main.rs`,
   Cargo.toml. Decide what belongs on `origin/main`.
3. Delete stale `codex/*` branches that pre-date Phase 3 closure.
4. Re-run `pnpm install && pnpm tauri build` to confirm toolchain.
5. **Audit `jira/client.rs` for hardcoded OAuth client IDs** before
   signing.

---

## Last known reference

| Field                       | Value                                                                                     |
| --------------------------- | ----------------------------------------------------------------------------------------- |
| `origin/main` tip           | `b503ea9` chore: add pull request template                                                |
| Last substantive commit     | `0283dd4` fix(security): harden release gates and sync correctness                        |
| Phase 3 status              | Closed (background scheduler + sync progress events delivered) per `PHASE3_STATUS.md`     |
| Default branch              | `main`                                                                                    |
| Build system                | Tauri 2 + Rust + React + TypeScript + SQLite                                              |
| Phase docs on `origin/main` | `PHASE3_PLAN.md`, `PHASE3_STATUS.md`                                                      |
| Release scaffolding         | **None on `origin/main`**                                                                 |
| Build verification status   | Untested in this pass — Cargo.toml is dirty locally                                       |
| Blocker                     | Apple signing + Jira credential model decision (operator-only)                            |
| Migration state             | **No `legacy-origin` remote** — clean from migration perspective                          |
| Local branch state          | **No `main` branch locally** — `master` (no upstream) + `codex/*` bootstrap branches only |
| Distinguishing feature      | **No local main branch** — fresh quirk shape for this session                             |
