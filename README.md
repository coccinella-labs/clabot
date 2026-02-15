# CLA Bot

Minimal GitHub Action to verify contributors have signed the Contributor License Agreement.

## Usage

Add this workflow to any repo:

```yaml
name: CLA

on:
  pull_request:
    types: [opened, synchronize, reopened]

jobs:
  cla:
    runs-on: ubuntu-latest
    steps:
      - uses: bniladridas/cla-bot@v1.2
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
          cla-url: https://your-site.com/cla.html
```

## Configuration

Edit `cla-signers.json` to add approved contributors:

```json
{
  "signed": [
    "octocat",
    "bniladridas",
    "infra-bot"
  ]
}
```

## Inputs

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| github-token | Yes | - | GitHub token for commenting on PRs |
| cla-url | No | - | URL to your CLA document |

## How it works

1. Runs on PR open/sync
2. Checks if PR author is in `cla-signers.json`
3. Passes silently if signed
4. Comments on PR with CLA link and fails if not signed
