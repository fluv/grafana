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

## Checking sync status after merge

After self-merging, verify Grafana accepted the dashboards:

```bash
curl -s http://10.43.66.208/apis/provisioning.grafana.app/v0alpha1/namespaces/default/repositories \
  | jq '.items[0].status.sync | {state, message}'
```

`state: "success"` is clean. `state: "warning"` means partial — read `message[]`
for the specific files that failed. Do not declare the merge done until the sync
state is clean or the warnings are understood and intentional.

Known benign warnings (ignore these):
- `folder ".github/" is missing folder metadata file` — Grafana sees the GitHub
  Actions directory as a potential dashboard folder. No action needed.
- `folder ".github/workflows/" is missing folder metadata file` — same as above.

Common failure modes:
- `cursorSync` must be a string (`"Off"`, `"Crosshair"`, `"Tooltip"`), not an integer
- A dashboard that already exists in Grafana's Postgres as "unmanaged" blocks Git
  from taking ownership — delete it via `DELETE /api/dashboards/uid/<uid>` first

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
