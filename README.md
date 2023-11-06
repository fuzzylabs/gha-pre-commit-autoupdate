# Pre-commit autoupdate

A Github action to run `pre-commit autoupdate`, run against all files and then 
raise a pull request if any updates are required.

## Example

```yaml
name: Pre-commit autoupdate

on: 
  # Run daily at midnight
  schedule:
    - cron: "0 0 * * *"
  # Allow a manual trigger
  workflow_dispatch:

jobs:
  auto-update:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      
      - uses: actions/setup-python@v2
        
      - uses: fuzzylabs/pre-commit-autoupdate-action@main
        
      - uses: peter-evans/create-pull-request@v5
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          branch: update/pre-commit-hooks
          title: Update pre-commit hooks
          commit-message: "Chore(deps): Upgrading `pre-commit` dependencies"
          body: Update version of `pre-commit` hooks to use latest version.
```
