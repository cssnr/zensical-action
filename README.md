[![GitHub Tag Major](https://img.shields.io/github/v/tag/cssnr/zensical-action?sort=semver&filter=!v*.*&logo=git&logoColor=white&labelColor=585858&label=%20)](https://github.com/cssnr/zensical-action/tags)
[![GitHub Tag Minor](https://img.shields.io/github/v/tag/cssnr/zensical-action?sort=semver&filter=!v*.*.*&logo=git&logoColor=white&labelColor=585858&label=%20)](https://github.com/cssnr/zensical-action/releases)
[![GitHub Release Version](https://img.shields.io/github/v/release/cssnr/zensical-action?logo=git&logoColor=white&labelColor=585858&label=%20)](https://github.com/cssnr/zensical-action/releases/latest)
[![Action Run Using](https://img.shields.io/badge/dynamic/yaml?url=https%3A%2F%2Fraw.githubusercontent.com%2Fcssnr%2Fzensical-action%2Frefs%2Fheads%2Fmaster%2Faction.yml&query=%24.runs.using&logo=githubactions&logoColor=white&label=runs)](https://github.com/cssnr/zensical-action/blob/master/action.yml)
[![Workflow Release](https://img.shields.io/github/actions/workflow/status/cssnr/zensical-action/release.yaml?logo=cachet&label=release)](https://github.com/cssnr/zensical-action/actions/workflows/release.yaml)
[![Workflow Lint](https://img.shields.io/github/actions/workflow/status/cssnr/zensical-action/lint.yaml?logo=cachet&label=lint)](https://github.com/cssnr/zensical-action/actions/workflows/lint.yaml)
[![GitHub Last Commit](https://img.shields.io/github/last-commit/cssnr/zensical-action?logo=github&label=updated)](https://github.com/cssnr/zensical-action/pulse)
[![Codeberg Last Commit](https://img.shields.io/gitea/last-commit/cssnr/zensical-action/master?gitea_url=https%3A%2F%2Fcodeberg.org%2F&logo=codeberg&logoColor=white&label=updated)](https://codeberg.org/cssnr/zensical-action)
[![GitHub Repo Size](https://img.shields.io/github/repo-size/cssnr/zensical-action?logo=bookstack&logoColor=white&label=repo%20size)](https://github.com/cssnr/zensical-action?tab=readme-ov-file#readme)
[![GitHub Contributors](https://img.shields.io/github/contributors-anon/cssnr/zensical-action?logo=github)](https://github.com/cssnr/zensical-action/graphs/contributors)
[![GitHub Discussions](https://img.shields.io/github/discussions/cssnr/zensical-action?logo=github)](https://github.com/cssnr/zensical-action/discussions)
[![GitHub Forks](https://img.shields.io/github/forks/cssnr/zensical-action?style=flat&logo=github)](https://github.com/cssnr/zensical-action/forks)
[![GitHub Repo Stars](https://img.shields.io/github/stars/cssnr/zensical-action?style=flat&logo=github)](https://github.com/cssnr/zensical-action/stargazers)
[![GitHub Org Stars](https://img.shields.io/github/stars/cssnr?style=flat&logo=github&label=org%20stars)](https://cssnr.github.io/)
[![Discord](https://img.shields.io/discord/899171661457293343?logo=discord&logoColor=white&label=discord&color=7289da)](https://discord.gg/wXy6m2X8wY)
[![Ko-fi](https://img.shields.io/badge/Ko--fi-72a5f2?logo=kofi&label=support)](https://ko-fi.com/cssnr)

# Zensical Action

<a title="Zensical Action" href="https://zensical-action.cssnr.com/" target="_blank">
<img alt="Zensical Action" align="right" width="128" height="auto" src="https://raw.githubusercontent.com/smashedr/repo-images/refs/heads/master/zensical-action/logo160.png"></a>

- [Features](#Features)
- [Inputs](#Inputs)
  - [Permissions](#Permissions)
- [Outputs](#Outputs)
- [Examples](#Examples)
  - [Repositories](#Repositories)
- [Tags](#Tags)
- [Support](#Support)
- [Contributing](#Contributing)

Zensical GitHub Action to checkout, build, upload, and deploy [Zensical Docs](https://github.com/zensical/zensical) to GitHub Pages.

Check out the [Features](#Features), [Inputs](#Inputs) and [Examples](#Examples) for options.

```yaml
name: 'Docs'
on:
  workflow_dispatch:
  push:
    branches: ['master']
jobs:
  docs:
    name: 'Docs'
    runs-on: ubuntu-latest
    permissions:
      pages: write
      id-token: write
    environment:
      name: github-pages
      url: ${{ steps.zensical.outputs.page_url }}
    steps:
      - name: 'Zensical Action'
        id: zensical
        uses: cssnr/zensical-action@v1
```

All steps can be disabled or customized, see the [Inputs](#Inputs) section for options.

For more details, see the [action.yml](https://github.com/cssnr/zensical-action/blob/master/action.yml).

## Features

- Build Docs
- Upload Artifact
- Deploy to Pages

More on the docs site: https://zensical-action.cssnr.com/

## Inputs

> [!TIP]
> View the [Getting Started](https://zensical-action.cssnr.com/) and [Usage Guide](https://zensical-action.cssnr.com/usage/) online.

All Inputs are **Optional**.

With no inputs the workflow reference is checked out, built, uploaded, and deployed to Pages.

| Input              | Default&nbsp;Value | Description&nbsp;of&nbsp;the&nbsp;Input                                                          |
| :----------------- | :----------------: | :----------------------------------------------------------------------------------------------- |
| **version**        |      _Latest_      | Zensial Version                                                                                  |
| **python-version** |     _Default_      | Python Version (see [setup-uv](https://github.com/astral-sh/setup-uv?tab=readme-ov-file#inputs)) |
| **uv-version**     |      _Latest_      | UV Version (see [setup-uv](https://github.com/astral-sh/setup-uv?tab=readme-ov-file#inputs))     |
| **directory**      |        `.`         | Build Directory (relative to root)                                                               |
| **path**           |       `site`       | Site Path (relative to root)                                                                     |
| **checkout**       |       `true`       | Runs: [actions/checkout](https://github.com/actions/checkout)                                    |
| [upload](#upload)  |   `github-pages`   | Upload: [`github-pages`,`artifact`,`false`]                                                      |
| [name](#name)      |     `artifact`     | Artifact Name if [upload](#upload) is `artifact`                                                 |
| [deploy](#deploy)  |       `true`       | Deploy to Pages (see [deploy](#deploy))                                                          |
| **summary**        |       `true`       | Add Job Summary to Workflow                                                                      |

#### upload

Determines the type of artifact uploaded. For a normal artifact use `artifact`.

Default: `github-pages`

#### name

Artifact Name if [upload](#upload) is set to `artifact`.

Default: `artifact`

#### deploy

This runs [actions/deploy-pages](https://github.com/actions/deploy-pages). Set to `false` to skip this.  
Make sure you have the required [permissions](#permissions).

If you set [upload](#upload) to anything except `github-pages` this step will be skipped.

Default: `true`

### Permissions

If you are deploying to GitHub Pages you need these permissions.

```yaml
permissions:
  pages: write
  id-token: write
```

Permissions documentation for [Workflows](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/controlling-permissions-for-github_token), [Actions](https://docs.github.com/en/actions/security-for-github-actions/security-guides/automatic-token-authentication), and [GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages).

## Outputs

| Output       | Description                                                                    |
| :----------- | :----------------------------------------------------------------------------- |
| **page_url** | Pages URL from [actions/deploy-pages](https://github.com/actions/deploy-pages) |
| **version**  | Zensical Version Used for Build                                                |
| **path**     | Site Path Used for Artifact                                                    |
| **name**     | Artifact [name](#name) from [upload](#upload) step                             |

The `path` will always be `site` or what you set for the input `path`.

```yaml
- name: 'Zensical Action'
  id: zensical
  uses: cssnr/zensical-action@v1

- name: 'Echo Output'
  run: |
    echo "page_url: ${{ steps.zensical.outputs.page_url }}"
    echo "version: ${{ steps.zensical.outputs.version }}"
    echo "path: ${{ steps.zensical.outputs.path }}"
    echo "name: ${{ steps.zensical.outputs.name }}"
```

## Examples

💡 _Click on an example heading to expand or collapse the example._

<details open><summary>Build and Deploy to GitHub Pages</summary>

```yaml
name: 'Docs'

on:
  workflow_dispatch:
  push:
    branches: [master]
    paths:
      - '.github/workflows/docs.yaml'
      - 'zensical.toml'
      - 'docs/**'

jobs:
  docs:
    name: 'Docs'
    runs-on: ubuntu-latest
    timeout-minutes: 5

    permissions:
      pages: write
      id-token: write

    environment:
      name: github-pages
      url: ${{ steps.zensical.outputs.page_url }}

    steps:
      - name: 'Zensical Action'
        id: zensical
        uses: cssnr/zensical-action@v1
```

</details>
<details><summary>Build and Deploy a Normal Artifact</summary>

```yaml
name: 'Docs'

on:
  workflow_dispatch:
  push:
    branches: [master]
    paths:
      - '.github/workflows/docs.yaml'
      - 'zensical.toml'
      - 'docs/**'

jobs:
  build:
    name: 'Build'
    runs-on: ubuntu-latest
    timeout-minutes: 5
    steps:
      - name: 'Zensical Action'
        uses: cssnr/zensical-action@v1
        with:
          upload: 'artifact'

  deploy:
    name: 'Deploy'
    uses: cssnr/workflows/.github/workflows/deploy-static.yaml@master
    needs: build
    with:
      name: github-pages
      url: https://dev-static.cssnr.com/
      robots: true
    secrets:
      host: ${{ secrets.DEV_DEPLOY_HOST }}
      port: ${{ secrets.DEV_DEPLOY_PORT }}
      user: ${{ secrets.DEV_DEPLOY_USER }}
      pass: ${{ secrets.DEV_DEPLOY_PASS }}
      webhook: ${{ secrets.DISCORD_WEBHOOK }}
    permissions:
      contents: read
```

</details>
<details><summary>Only Build the Site</summary>

```yaml
name: 'Docs'

on:
  workflow_dispatch:
  push:
    branches: [master]
    paths:
      - '.github/workflows/docs.yaml'
      - 'zensical.toml'
      - 'docs/**'

jobs:
  docs:
    name: 'Docs'
    runs-on: ubuntu-latest
    timeout-minutes: 5

    steps:
      - name: 'Zensical Action'
        id: zensical
        uses: cssnr/zensical-action@v1
        with:
          upload: false

      - name: 'Build Tree'
        run: |
          tree "${{ steps.zensical.outputs.path }}"
```

</details>

For more examples, you can check out other projects using this action:  
https://github.com/cssnr/zensical-action/network/dependents

### Repositories

Example repositories using this action to deploy to GitHub Pages.

| Repository&nbsp;Link                                                        |                                               Pages                                                |                                             Preview                                              | Website&nbsp;Link                                               |
| :-------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------: | :-------------------------------------------------------------- |
| [cssnr/zensical-action-docs](https://github.com/cssnr/zensical-action-docs) | [docs.yaml](https://github.com/cssnr/zensical-action-docs/blob/master/.github/workflows/docs.yaml) | [dev.yaml](https://github.com/cssnr/zensical-action-docs/blob/master/.github/workflows/dev.yaml) | [zensical-action.cssnr.com](https://zensical-action.cssnr.com/) |
| [cssnr/actions-tools](https://github.com/cssnr/actions-tools)               |    [docs.yaml](https://github.com/cssnr/actions-tools/blob/master/.github/workflows/docs.yaml)     |    [dev.yaml](https://github.com/cssnr/actions-tools/blob/master/.github/workflows/dev.yaml)     | [actions-tools.cssnr.com](https://actions-tools.cssnr.com/)     |

## Tags

The following rolling [tags](https://github.com/cssnr/zensical-action/tags) are maintained.

| Version&nbsp;Tag                                                                                                                                                                                               | Rolling | Bugs | Feat. |   Name    |  Target  | Example  |
| :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-----: | :--: | :---: | :-------: | :------: | :------- |
| [![GitHub Tag Major](https://img.shields.io/github/v/tag/cssnr/zensical-action?sort=semver&filter=!v*.*&style=for-the-badge&label=%20&color=44cc10)](https://github.com/cssnr/zensical-action/releases/latest) |   ✅    |  ✅  |  ✅   | **Major** | `vN.x.x` | `vN`     |
| [![GitHub Tag Minor](https://img.shields.io/github/v/tag/cssnr/zensical-action?sort=semver&filter=!v*.*.*&style=for-the-badge&label=%20&color=blue)](https://github.com/cssnr/zensical-action/releases/latest) |   ✅    |  ✅  |  ❌   | **Minor** | `vN.N.x` | `vN.N`   |
| [![GitHub Release](https://img.shields.io/github/v/release/cssnr/zensical-action?style=for-the-badge&label=%20&color=red)](https://github.com/cssnr/zensical-action/releases/latest)                           |   ❌    |  ❌  |  ❌   | **Micro** | `vN.N.N` | `vN.N.N` |

You can view the release notes for each version on the [releases](https://github.com/cssnr/zensical-action/releases) page.

The **Major** tag is recommended. It is the most up-to-date and always backwards compatible.
Breaking changes would result in a **Major** version bump. At a minimum you should use a **Minor** tag.

# Support

For general help or to request a feature, see:

- Q&A Discussion: https://github.com/cssnr/zensical-action/discussions/categories/q-a
- Request a Feature: https://github.com/cssnr/zensical-action/discussions/categories/feature-requests

If you are experiencing an issue/bug or getting unexpected results, you can:

- Report an Issue: https://github.com/cssnr/zensical-action/issues
- Chat with us on Discord: https://discord.gg/wXy6m2X8wY
- Provide General Feedback: [https://cssnr.github.io/feedback/](https://cssnr.github.io/feedback/?app=Update%20Release%20Notes)

For more information, see the CSSNR [SUPPORT.md](https://github.com/cssnr/.github/blob/master/.github/SUPPORT.md#support).

# Contributing

If you would like to submit a PR, please review the [CONTRIBUTING.md](#contributing-ov-file).

Please consider making a donation to support the development of this project
and [additional](https://cssnr.com/) open source projects.

[![Ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/cssnr)

[![Actions Tools](https://raw.githubusercontent.com/smashedr/repo-images/refs/heads/master/actions/actions-tools.png)](https://actions-tools.cssnr.com/)

Additionally, you can support other [GitHub Actions](https://actions.cssnr.com/) I have published:

- [Stack Deploy Action](https://github.com/cssnr/stack-deploy-action?tab=readme-ov-file#readme)
- [Portainer Stack Deploy Action](https://github.com/cssnr/portainer-stack-deploy-action?tab=readme-ov-file#readme)
- [Docker Context Action](https://github.com/cssnr/docker-context-action?tab=readme-ov-file#readme)
- [Actions Up Action](https://github.com/cssnr/actions-up-action?tab=readme-ov-file#readme)
- [Zensical Action](https://github.com/cssnr/zensical-action?tab=readme-ov-file#readme)
- [VirusTotal Action](https://github.com/cssnr/virustotal-action?tab=readme-ov-file#readme)
- [Mirror Repository Action](https://github.com/cssnr/mirror-repository-action?tab=readme-ov-file#readme)
- [Update Version Tags Action](https://github.com/cssnr/update-version-tags-action?tab=readme-ov-file#readme)
- [Docker Tags Action](https://github.com/cssnr/docker-tags-action?tab=readme-ov-file#readme)
- [Update JSON Value Action](https://github.com/cssnr/update-json-value-action?tab=readme-ov-file#readme)
- [JSON Key Value Check Action](https://github.com/cssnr/json-key-value-check-action?tab=readme-ov-file#readme)
- [Parse Issue Form Action](https://github.com/cssnr/parse-issue-form-action?tab=readme-ov-file#readme)
- [Cloudflare Purge Cache Action](https://github.com/cssnr/cloudflare-purge-cache-action?tab=readme-ov-file#readme)
- [Mozilla Addon Update Action](https://github.com/cssnr/mozilla-addon-update-action?tab=readme-ov-file#readme)
- [Package Changelog Action](https://github.com/cssnr/package-changelog-action?tab=readme-ov-file#readme)
- [NPM Outdated Check Action](https://github.com/cssnr/npm-outdated-action?tab=readme-ov-file#readme)
- [Label Creator Action](https://github.com/cssnr/label-creator-action?tab=readme-ov-file#readme)
- [Algolia Crawler Action](https://github.com/cssnr/algolia-crawler-action?tab=readme-ov-file#readme)
- [Upload Release Action](https://github.com/cssnr/upload-release-action?tab=readme-ov-file#readme)
- [Check Build Action](https://github.com/cssnr/check-build-action?tab=readme-ov-file#readme)
- [Web Request Action](https://github.com/cssnr/web-request-action?tab=readme-ov-file#readme)
- [Get Commit Action](https://github.com/cssnr/get-commit-action?tab=readme-ov-file#readme)

<details><summary>❔ Unpublished Actions</summary>

These actions are not published on the Marketplace, but may be useful.

- [cssnr/create-files-action](https://github.com/cssnr/create-files-action?tab=readme-ov-file#readme) - Create various files from templates.
- [cssnr/draft-release-action](https://github.com/cssnr/draft-release-action?tab=readme-ov-file#readme) - Keep a draft release ready to publish.
- [cssnr/env-json-action](https://github.com/cssnr/env-json-action?tab=readme-ov-file#readme) - Convert env file to json or vice versa.
- [cssnr/push-artifacts-action](https://github.com/cssnr/push-artifacts-action?tab=readme-ov-file#readme) - Sync files to a remote host with rsync.
- [smashedr/update-release-notes-action](https://github.com/smashedr/update-release-notes-action?tab=readme-ov-file#readme) - Update release notes.
- [smashedr/combine-release-notes-action](https://github.com/smashedr/combine-release-notes-action?tab=readme-ov-file#readme) - Combine release notes.

---

</details>

<details><summary>📝 Template Actions</summary>

These are basic action templates that I use for creating new actions.

- [javascript-action](https://github.com/smashedr/javascript-action?tab=readme-ov-file#readme) - JavaScript
- [typescript-action](https://github.com/smashedr/typescript-action?tab=readme-ov-file#readme) - TypeScript
- [py-test-action](https://github.com/smashedr/py-test-action?tab=readme-ov-file#readme) - Dockerfile Python
- [test-action-uv](https://github.com/smashedr/test-action-uv?tab=readme-ov-file#readme) - Dockerfile Python UV
- [docker-test-action](https://github.com/smashedr/docker-test-action?tab=readme-ov-file#readme) - Docker Image Python

Note: The `docker-test-action` builds, runs and pushes images to [GitHub Container Registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry).

---

</details>

For a full list of current projects visit: [https://cssnr.github.io/](https://cssnr.github.io/)
