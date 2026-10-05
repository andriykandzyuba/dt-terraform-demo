# dt-terraform-demo
Dynatrace Terraform Provider Demo

## Setup

## Prerequisite: 

Install Terraform CLI `terraform`.

## Initialize the Terraform working directory:

1. Configure a new Dynatrace OAuth Client with the following scopes:

```aiignore
document:documents:write
document:documents:read
document:documents:delete
document:trash.documents:delete
slo:slos:read
slo:slos:write
```

2. Set environent variables for your Dynatrace environment and OAuth client credentials to **.env.sh** file:

```bash
export DYNATRACE_ENV_URL=https://<tenant_id>.live.dynatrace.com
export DT_CLIENT_ID=...
export DT_CLIENT_SECRET=...
export DT_ACCOUNT_ID=...
export DYNATRACE_MAX_HTTP_WORKERS=30
```

3. Source the environment variables:

```bash
source ./.env.sh
```

4. Initialize the Terraform working directory:

```bash
terraform init
``` 

5. Ensure the Dynatrace Terraform Provider CLI is downloaded:
```bash
ls -las  .terraform/providers/registry.terraform.io/dynatrace-oss/dynatrace/1.105.0/darwin_arm64
```
6. Export this provider to your PATH:

```bash
export PATH=$PATH:$(pwd)/.terraform/providers/registry.terraform.io/dynatrace-oss/dynatrace/1.105.0/darwin_arm64
```
7. Create an alias for the provider in your shell:

```bash
alias terraform-provider-dynatrace=$(pwd)/.terraform/providers/registry.terraform.io/dynatrace-oss/dynatrace/1.105.0/darwin_arm64
```

## Export Dashboard and SLO configurations from Dynatrace environment

1. Run the export command to export dashboard and SLO configurations from your Dynatrace environment:

```bash
erraform-provider-dynatrace -export -import-state dynatrace_platform_slo
```

2. Wait for a few minutes until the export is completed. The exported configurations will be saved in the `configuration` directory.

3. Explore the configurations files. 

## Modify and apply the exported configurations to a new Dynatrace environment

1. 