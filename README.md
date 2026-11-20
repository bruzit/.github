# BruzIT Organization

[![License](https://img.shields.io/github/license/bruzit/.github)](LICENSE)
[![Last commit](https://img.shields.io/github/last-commit/bruzit/.github)](https://github.com/bruzit/.github/commits)
[![MegaLinter](https://github.com/bruzit/.github/actions/workflows/megalinter.yaml/badge.svg)](https://github.com/bruzit/.github/actions/workflows/megalinter.yaml)
[![Terraform Plan](https://github.com/bruzit/.github/actions/workflows/terraform-plan.yaml/badge.svg)](https://github.com/bruzit/.github/actions/workflows/terraform-plan.yaml)
[![Semantic Release](https://github.com/bruzit/.github/actions/workflows/semantic-release.yaml/badge.svg)](https://github.com/bruzit/.github/actions/workflows/semantic-release.yaml)
[![Terraform](https://github.com/bruzit/.github/actions/workflows/terraform.yaml/badge.svg)](https://github.com/bruzit/.github/actions/workflows/terraform.yaml)

BruzIT organization profile and the declarative YAML definition of its repositories, reconciled into GitHub by GitHub Organization as Code.

## Features

- **[BruzIT GitHub Organization](https://github.com/bruzit) management** - Defined as code in [`bruzit.yaml`](bruzit.yaml), provisioned with [BruzIT GitHub Organization as Code](https://github.com/bruzit/github-organization-as-code).
- **Organization profile** - The public front page of the BruzIT GitHub Organization: [`profile/README.md`](profile/README.md).

## Requirements

- [BruzIT GitHub Organization as Code](https://github.com/bruzit/github-organization-as-code) cloned next to this repository; `TF_VAR_config` in [`.env.tmpl`](.env.tmpl) points from its `terraform` directory to `../../.github/bruzit.yaml`.
- Terraform `~> 1.15`.
- direnv, which loads [`.envrc`](.envrc) into your shell.
- An S3-compatible bucket for the Terraform state, and GitHub Apps with plan (read-only) and apply credentials.

## Installation and Setup

Copy [`.env.tmpl`](.env.tmpl), [`.env.plan.tmpl`](.env.plan.tmpl) and [`.env.apply.tmpl`](.env.apply.tmpl) to the same names without `.tmpl`, fill them in, then initialize Terraform:

```shell
terraform -chdir=../github-organization-as-code/terraform init -backend-config="bucket=$AWS_BUCKET"
```

## Usage

Plan by default: direnv loads the read-only plan credentials. To apply, prefix a single command with `TF_MODE=apply`; only that command gets the apply credentials.

```shell
terraform -chdir=../github-organization-as-code/terraform plan -lock=false -refresh=false
TF_MODE=apply direnv exec . terraform -chdir=../github-organization-as-code/terraform apply
```

## Support

[Open a GitHub issue](../../issues). I answer best effort, as a community project.

## Integration and Deployment

| Workflow                                                                   | Trigger                           | Purpose                                                                                                       |
|----------------------------------------------------------------------------|-----------------------------------|---------------------------------------------------------------------------------------------------------------|
| [`megalinter.yaml`](.github/workflows/megalinter.yaml)                     | Pull request                      | Lint changed files with MegaLinter, autofix via app; required check.                                          |
| [`terraform-plan.yaml`](.github/workflows/terraform-plan.yaml)             | Pull request                      | Terraform plan of [`bruzit.yaml`](bruzit.yaml) against the organization (`plan` environment); required check. |
| [`semantic-release.yaml`](.github/workflows/semantic-release.yaml)         | Push to `main`                    | Version, changelog and GitHub release by semantic-release (`release` environment).                            |
| [`terraform.yaml`](.github/workflows/terraform.yaml)                       | Push to `main`, manual            | Terraform apply of [`bruzit.yaml`](bruzit.yaml) (`production` environment).                                   |
| [`megalinter-scheduled.yaml`](.github/workflows/megalinter-scheduled.yaml) | Weekly (Monday 06:00 UTC), manual | Lint the whole codebase with MegaLinter.                                                                      |

A push to `main` applies [`bruzit.yaml`](bruzit.yaml) to the live BruzIT GitHub Organization (`production` environment).

## Contributing

Open a pull request to `main`. Write commits per the [Conventional Commits 1.0.0 specification](https://www.conventionalcommits.org/en/v1.0.0/); semantic-release sets the version and changelog from them.

## License and Copyright

MIT License: [`LICENSE`](LICENSE)  
Copyright © 2026 Martin Bružina

## Stats

| Metric           | Badges                                                                                                                                                                                                                                                                                                                                                                                                                             |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Commits          | [![Commits total](https://img.shields.io/github/commit-activity/t/bruzit/.github?label=commits%20total)](https://github.com/bruzit/.github/commits/main)                                                                                                                                                                                                                                                                           |
| Issues           | [![Issues open](https://img.shields.io/github/issues/bruzit/.github?label=issues)](https://github.com/bruzit/.github/issues) [![Issues total](https://img.shields.io/github/issues-search?query=repo%3Abruzit%2F.github%20is%3Aissue&label=issues%20total)](https://github.com/bruzit/.github/issues?q=is%3Aissue)                                                                                                                 |
| Pull requests    | [![Pull requests open, not draft](https://img.shields.io/github/issues-search?query=repo%3Abruzit%2F.github%20is%3Apr%20is%3Aopen%20draft%3Afalse&label=PRs%20open)](https://github.com/bruzit/.github/pulls?q=is%3Apr+is%3Aopen+draft%3Afalse) [![Pull requests total](https://img.shields.io/github/issues-search?query=repo%3Abruzit%2F.github%20is%3Apr&label=PRs%20total)](https://github.com/bruzit/.github/pulls?q=is%3Apr) |
| Checks on `main` | [![Checks on main](https://img.shields.io/github/check-runs/bruzit/.github/main?label=checks%20%28main%29)](https://github.com/bruzit/.github/actions?query=branch%3Amain)                                                                                                                                                                                                                                                         |
| Releases         | [![Latest release](https://img.shields.io/github/v/release/bruzit/.github)](https://github.com/bruzit/.github/releases/latest) [![Commits since latest release](https://img.shields.io/github/commits-since/bruzit/.github/latest)](https://github.com/bruzit/.github/releases)                                                                                                                                                    |
| Community        | [![Stargazers](https://img.shields.io/github/stars/bruzit/.github)](https://github.com/bruzit/.github/stargazers) [![Forks](https://img.shields.io/github/forks/bruzit/.github)](https://github.com/bruzit/.github/forks) [![Contributors](https://img.shields.io/github/contributors/bruzit/.github)](https://github.com/bruzit/.github/graphs/contributors)                                                                      |
