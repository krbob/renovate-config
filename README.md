# Shared Renovate configuration

Reusable Renovate presets for repositories owned by `krbob`.

## Presets

- `github>krbob/renovate-config:common` — shared non-policy defaults for repositories that
  need their own cadence or automerge rules.
- `github>krbob/renovate-config` or `github>krbob/renovate-config:monthly` — create and
  automerge all mature dependency updates on the first day of each month. Creation is not
  concurrency-limited, GitHub merges each pull request as soon as required CI passes, and
  Renovate may refresh an existing branch after day 1, including for a newer eligible release
  or when a real conflict must be resolved; it does not create a new branch outside day 1.
- `github>krbob/renovate-config:monthly-private` — the same monthly creation policy for private
  repositories where GitHub platform automerge and required-status rules are unavailable;
  Renovate's own automerge may continue draining the queue after day 1.
- `github>krbob/renovate-config:continuous` — create and automerge updates continuously for
  repositories with few dependencies.

Repository-specific managers, grouping, version constraints, and exceptional release trains stay
in each repository's own Renovate configuration.

The monthly preset disables Renovate's special `vulnerabilityAlerts` pull requests because those
ignore `schedule`. Vulnerable dependencies are still included in the normal monthly update run.

## Validation

```bash
npx --yes renovate renovate-config-validator --no-global \
  default.json common.json base.json monthly.json monthly-private.json continuous.json
```
