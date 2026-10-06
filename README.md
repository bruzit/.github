# BruzIT Organization

BruzIT organization profile and the declarative YAML definition of its repositories, reconciled into GitHub by GitHub Organization as Code.

## Features

- **[BruzIT GitHub Organization](https://github.com/bruzit) management** - Defined as code in [`bruzit.yaml`](bruzit.yaml) and provisioned using [BruzIT / GitHub Organization as Code](https://github.com/bruzit/github-organization-as-code).

## Local Usage

Copy the templates [`.env.tmpl`](.env.tmpl), [`.env.plan.tmpl`](.env.plan.tmpl) and [`.env.apply.tmpl`](.env.apply.tmpl) without `.tmpl` and fill them in. Direnv loads plan mode with read-only credentials by default, apply credentials only for a single command with `TF_MODE=apply`.

```shell
terraform -chdir=../github-organization-as-code/terraform init -backend-config="bucket=$AWS_BUCKET"
terraform -chdir=../github-organization-as-code/terraform plan -lock=false -refresh=false
TF_MODE=apply direnv exec . terraform -chdir=../github-organization-as-code/terraform apply
```

## Copyright and Licensing

[MIT License](LICENSE)  
Copyright © 2026 Martin Bružina
