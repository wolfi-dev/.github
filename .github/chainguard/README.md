# Production export-wolfi trust

Publication writes only wolfi-dev/os; the export identity has no public-write grant.

These policies are part of [OS-2867](https://linear.app/chainguard/issue/OS-2867).
Follow the [production runbook](https://github.com/chainguard-dev/mono/blob/main/env/enforce.dev/iac/400-export-wolfi/README.md).

Merge after staging memory acceptance and paused production infrastructure
provisioning. Replace each `UNPROVISIONED-...` subject with the created account's
numeric `uniqueId` from the stage's `octosts_policies` output; re-run policy checks
and obtain review before merge. The placeholder deliberately matches no Google
service account and must never be treated as a working runtime grant.

The three runtime-policy PRs can merge in parallel once their exact subjects are
reviewed. Keep both new schedules paused while installing grants. Complete the
single-writer handover and signed-history proof before merging activation. Runtime
accounts have no git-export access; mono's existing build policy handles direct ko.
