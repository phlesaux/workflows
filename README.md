## Reusable GitHub Actions Workflows

### `dependabot-auto-merge.yml`

Auto-merges Dependabot PRs.\
Patch and minor updates are auto-merged by default.\
Majors are left for manual review.

| Input | Default | Description |
| --- | --- | --- |
| `auto_merge_major` | `false` | Auto-merge major version updates |
| `auto_merge_minor` | `true` | Auto-merge minor version updates |
| `auto_merge_patch` | `true` | Auto-merge patch version updates |

```yaml
on:
  pull_request:

permissions:
  contents: write
  pull-requests: write

jobs:
  auto-merge:
    uses: phlesaux/workflows/.github/workflows/dependabot-auto-merge.yml@v1
```

To auto-merge majors as well, pass `with: auto_merge_major: true`.

### `secret-scan.yml`

Runs [gitleaks](https://github.com/gitleaks/gitleaks) over the full Git history.

| Input | Default | Description |
| --- | --- | --- |
| `config-path` | `""` | gitleaks config file; empty uses the default ruleset |
| `fetch-depth` | `0` | Commits to fetch; `0` fetches the full history |

```yaml
on:
  pull_request:
  push:
    branches: [main]

permissions:
  contents: read

jobs:
  secret-scan:
    uses: phlesaux/workflows/.github/workflows/secret-scan.yml@v1
```

### `validate-compose.yml`

Copies the env template to `.env` and runs `docker compose config -q`.\
If the template is missing, validation runs without `.env`.\
Required variables will still fail the check.

| Input | Default | Description |
| --- | --- | --- |
| `compose-file` | `compose.yaml` | Compose file to validate |
| `env-file` | `.env.dist` | Environment template copied to `.env` |

```yaml
on:
  pull_request:

permissions:
  contents: read

jobs:
  validate:
    uses: phlesaux/workflows/.github/workflows/validate-compose.yml@v1
```

Override the defaults with `with:` when a project uses different filenames.
