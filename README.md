[![StepSecurity Maintained Action](https://raw.githubusercontent.com/step-security/maintained-actions-assets/main/assets/maintained-action-banner.png)](https://docs.stepsecurity.io/actions/stepsecurity-maintained-actions)

<p align="right">
  <a href="https://github.com/step-security/github-action-auto-release/releases/latest"><img src="https://img.shields.io/github/release/step-security/github-action-auto-release.svg?style=for-the-badge" alt="Latest Release"/></a>
  <a href="https://github.com/step-security/github-action-auto-release/commits"><img src="https://img.shields.io/github/last-commit/step-security/github-action-auto-release.svg?style=for-the-badge" alt="Last Updated"/></a>
</p>

This is an opinionated composite Github Action that implements a workflow based on the popular `release-drafter` action to automatically draft releases with release notes that are derived from PR descriptions as they are merged into the default branch.

Under default settings, `auto-release` will also cut a new release from the default branch after every merge into it. However, releases are not cut for merges of pull requests with a `no-release` label attached. In that case, the release notes are left as a draft and a release with all unreleased changes will be made the next time a pull request without the `no-release` label is merged into the default branch.







## Usage

Add this action as a step in your workflow. It runs as per your configuration and automatically drafts or publishes a release based on merged pull requests.

```yaml
- uses: step-security/github-action-auto-release@v1
  with:
    token: ${{ secrets.GITHUB_TOKEN }}
    publish: "true"
```

The action reads its release-drafter config from `.github/configs/draft-release.yml` by default. You can override this with the `config-name` input.

## Quick Start

1. Create a workflow file in your repo, e.g. `.github/workflows/release.yml`:

```yaml
name: Release

on:
  push:
    branches: [main]

jobs:
  release:
    runs-on: ubuntu-latest
    permissions:
      contents: write
      pull-requests: read
    steps:
      - uses: step-security/github-action-auto-release@v1
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          publish: "true"
```

2. Create a release-drafter config at `.github/configs/draft-release.yml`. Refer to the [release-drafter configuration docs](https://github.com/step-security/release-drafter#configuration) for available options.


## Inputs
<!-- markdownlint-disable -->
| Name | Description | Default | Required |
|------|-------------|---------|----------|
| config-name | If your workflow requires multiple release-drafter configs it is helpful to override the config-name.<br>The config should still be located inside `.github` as that's where we are looking for config files.<br> | configs/draft-release.yml | false |
| latest | A string indicating whether the release being created or updated should be marked as latest.<br> |  | false |
| prerelease | Boolean indicating whether this release should be a prerelease |  | false |
| publish | Whether to publish a new release immediately | false | false |
| summary-enabled | Enable github action summary. | true | false |
| token | Standard GitHub token (e.g., secrets.GITHUB\_TOKEN) | ${{ github.token }} | false |
<!-- markdownlint-restore -->


## Outputs
<!-- markdownlint-disable -->
| Name | Description |
|------|-------------|
| body | The body of the drafted release. |
| exists | Tag exists so skip new release issue |
| html\_url | The URL users can navigate to in order to view the release |
| id | The ID of the release that was created or updated. |
| major\_version | The next major version number. For example, if the last tag or release was v1.2.3, the value would be v2.0.0. |
| minor\_version | The next minor version number. For example, if the last tag or release was v1.2.3, the value would be v1.3.0. |
| name | The name of the release |
| patch\_version | The next patch version number. For example, if the last tag or release was v1.2.3, the value would be v1.2.4. |
| resolved\_version | The next resolved version number, based on GitHub labels. |
| tag\_name | The name of the tag associated with the release. |
| upload\_url | The URL for uploading assets to the release, which could be used by GitHub Actions for additional uses, for example the @actions/upload-release-asset GitHub Action. |
<!-- markdownlint-restore -->

## References

- [Release Drafter](https://github.com/step-security/release-drafter) - Drafts your next release notes as pull requests are merged into master

For 🐛 bug reports & feature requests, please use the [issue tracker](https://github.com/step-security/github-action-auto-release/issues).

## License

<a href="https://opensource.org/licenses/Apache-2.0"><img src="https://img.shields.io/badge/License-Apache%202.0-blue.svg?style=for-the-badge" alt="License"></a>

Copyright © 2022-2026 [Cloud Posse, LLC](https://cloudposse.com)

Copyright 2026 StepSecurity


Licensed under the Apache License, Version 2.0. See [LICENSE](./LICENSE) for details.
