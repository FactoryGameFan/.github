# .github

Org-wide defaults for the FactoryGameFan organization.

## `renovate-config.json`

The shared [Renovate](https://docs.renovatebot.com/) preset. Every repo in the org that has
dependencies pulls it in with:

```json
{
  "extends": ["local>FactoryGameFan/.github:renovate-config"]
}
```

It holds the settings that are the same everywhere: the timezone, the weekly Monday batch,
`automerge: false`, the PR rate caps, the rule that security fixes skip the weekly window, and
the GitHub Actions grouping.

It deliberately does **not** hold release-age floors, lockfile maintenance, or package holds.
Those differ per repo and their reasoning is written next to them in each repo's own config.
`FactorioMapWebUI` and `FactorioTools` set opposite values for `lockFileMaintenance`, and both
are correct for their repo.

### Before you edit it

- Validate with `npx --package renovate -- renovate-config-validator renovate-config.json`.
  Run it from outside a project root; a bare `npx` inside one can fail with `EBADDEVENGINES`.
- A repo running with the app's "Require config file" setting does nothing, silently, if its
  config fails to resolve. A broken preset here reads as "no updates available", not as an error.
- This repo must stay ticked in the Renovate app installation, or no repo can read the preset.

### Which repos use it

| Repo | Managers |
| --- | --- |
| `FactorioMapWebUI` | pnpm, cargo, github-actions |
| `FactorioTools` | npm, github-actions |
| `factorio-blueprint-editor` | npm, cargo, github-actions |
| `factorio-oracle` | cargo, github-actions |
| `factorygamefan` | npm |

`FactorioWikiDamageThresholds` and the archived `Factorio-Blueprints` have no dependency
manifests, so Renovate has nothing to do in them.
