# Automated Pre-Commit Updates

A GitHub action to run `pre-commit autoupdate` and run against all files.

Can be used in workflow to raise a pull request if any updates are required.

This action will:

1. Checkout the caller repository and set up Python.
2. Install pre-commit using `pip`.
3. Run `pre-commit autoupdate`.
4. Run `pre-commit` to ensure that all pre-commit checks pass after update.
5. Create a PR 

## Action inputs

This action takes python version as an **optional** input, defaulting to 3.10.12 if no input is given.

| Name | Description                                                                         | Default |
| --- |-------------------------------------------------------------------------------------| --- |
| `python-version` | The python version to use with pre-commit, the minimum version required is >=3.10.5 | 3.10.12 |

## Example

The following is an example of how this action might be used in a workflow.

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
      - uses: fuzzylabs/pre-commit-autoupdate-action@main
        with:
          python_version: "3.10.12"
```
