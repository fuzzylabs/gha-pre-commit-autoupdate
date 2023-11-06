# Pre-commit autoupdate

A Github action to run `pre-commit autoupdate` and run against all files.

Can be used in workflow to raise a pull request if any updates are required.

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
      - uses: actions/checkout@v4
      
      - uses: actions/setup-python@v4
        with:
          python-version: '3.10'
        
      - uses: fuzzylabs/pre-commit-autoupdate-action@main
        
      - uses: peter-evans/create-pull-request@v5
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          branch: update/pre-commit-hooks
          title: Update pre-commit hooks
          commit-message: "Chore(deps): Upgrading `pre-commit` dependencies"
          body: Update version of `pre-commit` hooks to use latest version.
```
