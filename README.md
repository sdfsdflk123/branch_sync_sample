# main to develop sync

This repo demonstrates a GitHub Actions flow that merges `main` into `develop` after a `main` push.

## Workflows

- `.github/workflows/sync-main-to-develop.yml`: triggers on `main` push and calls the reusable workflow.
- `.github/workflows/sync-base-to-develop.reusable.yml`: creates a GitHub App token, checks out `develop`, merges `main`, and pushes `develop`.

## Required secrets

- `SYNC_DEVELOP_APP_ID`
- `SYNC_DEVELOP_APP_PRIVATE_KEY`

## GitHub App setup

1. Create a GitHub App in the organization.
2. Set repository permissions:
   - `Contents`: Read and write
   - `Metadata`: Read-only
3. Install the app only on the target repositories.
4. Add the app to the `develop` branch ruleset or branch protection bypass list.

## Notes

- The reusable workflow uses `actions/create-github-app-token@v1`.
- If `develop` has a protection rule that blocks direct pushes, the app must be allowed to bypass it.
