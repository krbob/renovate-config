# Shared Renovate configuration

Reusable Renovate presets for repositories owned by `krbob`.

## Presets

- `github>krbob/renovate-config:common` — shared non-policy defaults for repositories that
  need their own cadence or automerge rules.
- `github>krbob/renovate-config` or `github>krbob/renovate-config:monthly` — create and
  automerge all mature dependency updates on the first day of each month. At most five pull
  requests are open at once and GitHub merges each one as soon as required CI passes.
- `github>krbob/renovate-config:monthly-private` — the same monthly policy for private
  repositories where GitHub platform automerge and required-status rules are unavailable.
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
