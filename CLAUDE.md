# CLAUDE.md — zuzak/grafana

Dashboard JSON files for the homelab Grafana instance. Grafana pulls from
this repo every 60 seconds via Git sync; a merge to main is live within a minute.

## Self-merge permission

Read-only content in this repo — dashboard JSON files, README, this file —
may be merged without human review. Claude is authorised to:

- Add or update dashboard JSON files
- Fix datasource UIDs, labels, or panel descriptions
- Create a branch, push, open a PR, and merge it immediately
- No vet round required; no waiting for Douglas

Changes that need human review:
- Anything that affects Grafana's provisioning or cluster configuration (those
  live in `zuzak/kube`, not here)
- Adding credentials or sensitive data (which must never appear in this repo)

The pre-push hook still blocks direct-to-main for all repos; the workflow is
branch → push → `gh pr create` → `gh pr merge --merge` in the same session.

Before merging, run `pre-commit run --all-files` locally and fix any failures.
The CI runs the same check on every push to main — merging a broken build
breaks the pipeline for subsequent commits. Self-merge permission does not
override this gate: a PR that would fail CI must not be merged.

## Datasource UIDs

| Datasource | UID |
|---|---|
| Prometheus | `prometheus` |
| Loki | `loki` |

Community dashboards often hardcode UIDs from the author's instance. Check and
fix before committing (see README for per-file notes).

## Attribution

Add a row to the README attribution table for any new community dashboard. Note
the source URL, author, and license. Apache-2.0 and CC BY-SA 4.0 are the common
ones; "no license declared" is acceptable to note but means use with caution.
