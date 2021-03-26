# Release Tester

Helper project to test automated release processes using Github Actions

## Requirements

An `SSH-Key` is required that is stored under the secret: `SSH_PRIVATE_KEY`.

## Assumptions

This repo assumes
 * has a `main` branch
 * has a `dev` branch

## Release Process

1. go to https://github.com/sgratzl/release-tester/actions/workflows/create_release.yml and trigger a manual release build. You can specify which version should be used or a magic word like `patch` to create a patch release
1. the action will create a PR trying to merge latest `dev` changes + version update to `main`
1. once approved and merged the regular `main` branch action will be triggered

## Push

On every `push` an CI jobs runs building and testing things.

### Push to Main

1. determine which version is currently used
1. Create a GitHub Release for this version and tag it
1. Build and Upload Assets
1. Create a PR that is merging `main` changes back to `dev`

#### Push to dev or a tag (v...)

After the regular build has completed it will create a new docker build and pushed it to the registry
