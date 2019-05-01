# terraform-provider-ansible-vault

## Usage

```tf
provider "ansiblevault" {
  vault_pass = "~/.vault_pass.txt"
  root_folder = "~/infra/ansible/"
}

resource "ansiblevault_env" "api_key" {
  env    = "prod"
  value  = "SECRET_API_KEY"
}

${ansiblevault_env.api_key.value}
```
