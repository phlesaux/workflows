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
