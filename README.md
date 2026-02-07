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
      - uses: bniladridas/cla-bot@v1
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
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

## How it works

1. Runs on PR open/sync
2. Checks if PR author is in `cla-signers.json`
3. Passes silently if signed
4. Comments on PR and fails if not signed
