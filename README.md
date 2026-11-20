# Shared Renovate preset

Shared dependency update policy for Dunklas repositories.

## Usage

Add a `renovate.json` to each service:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>Dunklas/renovate"]
}
```

Renovate must also be enabled for the consuming repository.
Consumers follow this repository's default branch, so merged preset changes
apply on their next Renovate run. Add repository-specific settings alongside
`extends` when needed.

## Policy

- Extend `config:recommended`.
- Schedule updates for Mondays, 00:00–05:59 UTC, with updates outside that window disabled.
- Limit concurrent dependency PRs to six.
- Allow vulnerability alert updates outside the schedule.
- Group minor and patch updates by manager.
- Track .NET SDK versions in mise and `dotnet-ef` versions in Dockerfiles.
- Group .NET SDK/container updates and EF Core updates separately.

The .NET-specific rules only apply when matching dependencies are present.

## Validation

With Node.js 24.11 or newer in the Node.js 24 release line:

```sh
npx --yes --package renovate@44.256.0 -- renovate-config-validator --no-global --strict default.json
```

GitHub Actions runs the same validation on pull requests and pushes to `main`.
