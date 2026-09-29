# Production export-wolfi trust

Publication writes only wolfi-dev/os; the export identity has no public-write grant.

These policies are part of [OS-2867](https://linear.app/chainguard/issue/OS-2867).
Follow the [production runbook](https://github.com/chainguard-dev/mono/blob/main/env/enforce.dev/iac/400-export-wolfi/README.md).

Merge after staging memory acceptance and confirmed paused production
infrastructure deployment. These policies bind dedicated production service
accounts by their numeric `uniqueId`. Reconfirm the subjects against the stage's
`octosts_policies` output and obtain review before merge. If an account is
recreated, update its exact subject and repeat the policy checks and review.

The three runtime-policy PRs can merge in parallel once their exact subjects are
reviewed. Keep both new schedules paused while installing grants. Complete the
single-writer handover and signed-history proof before merging activation. Runtime
accounts have no git-export access; mono's existing build policy handles direct ko.
