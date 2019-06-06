# terraform-provider-ansiblevault

[![Build Status](https://travis-ci.org/MeilleursAgents/terraform-provider-ansiblevault.svg?branch=master)](https://travis-ci.org/MeilleursAgents/terraform-provider-ansiblevault)
[![codecov](https://codecov.io/gh/MeilleursAgents/terraform-provider-ansiblevault/branch/master/graph/badge.svg)](https://codecov.io/gh/MeilleursAgents/terraform-provider-ansiblevault)
[![Go Report Card](https://goreportcard.com/badge/github.com/MeilleursAgents/terraform-provider-ansiblevault)](https://goreportcard.com/report/github.com/MeilleursAgents/terraform-provider-ansiblevault)

## Thanks

Thanks to [ansible-vault-go](github.com/sosedoff/ansible-vault-go) repository for have done the hardest part.

## Installation

If you have [Golang installed](https://golang.org/dl/)

```bash
go install github.com/MeilleursAgents/terraform-provider-ansiblevault
mkdir -p "~/.terraform.d/plugins/$(go env GOHOSTOS)_$(go env GOHOSTARCH)/"
cp ${GOPATH}/bin/terraform-provider-ansiblevault "~/.terraform.d/plugins/$(go env GOHOSTOS)_$(go env GOHOSTARCH)/"
```

Without golang

```bash
PLUGIN_VERSION="1.0.1"
OS=$(uname -s | tr '[:upper:]' '[:lower:]')
ARCH=$(uname -m | tr '[:upper:]' '[:lower:]')

if [[ "${ARCH}" = "x86_64" ]]; then
  ARCH="amd64"
fi

mkdir -p "~/.terraform.d/plugins/${OS}_${ARCH}/"
curl -O "https://github.com/MeilleursAgents/terraform-provider-ansiblevault/releases/download/v${PLUGIN_VERSION}/terraform-provider-ansiblevault_v${PLUGIN_VERSION}"
```

## Usage

ansiblevault_env example:

---

```tf
provider "ansiblevault" {
  vault_pass  = "/home/username/.vault_pass.txt"
  root_folder = "/home/username/infra/ansible/"
}

data "ansiblevault_env" "api_key" {
  env = "prod"
  key = "SECRET_API_KEY"
}

${data.ansiblevault_env.api_key.value}
```

ansiblevault_path example:

---

```tf
provider "ansiblevault" {
  vault_pass  = "/home/username/.vault_pass.txt"
  root_folder = "/home/username/infra/ansible/"
}

data "ansiblevault_path" "api_key" {
  path = "./passwords.yml"
  key = "USER_PASSWORD"
}

${data.ansiblevault_path.api_key.value}
```

## Contribution

You have to enable [Go modules](https://github.com/golang/go/wiki/Modules) for compiling this project.
