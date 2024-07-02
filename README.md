# terraform-azurerm-openai
Azure OpenAI Terraform Module and Samples


<!-- BEGIN_TF_DOCS -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 1.3.0 |
| <a name="requirement_azurerm"></a> [azurerm](#requirement\_azurerm) | ~> 3.80 |
| <a name="requirement_modtm"></a> [modtm](#requirement\_modtm) | >= 0.1.8, < 1.0 |
| <a name="requirement_random"></a> [random](#requirement\_random) | >= 3.0 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_azurerm"></a> [azurerm](#provider\_azurerm) | ~> 3.80 |
| <a name="provider_modtm"></a> [modtm](#provider\_modtm) | >= 0.1.8, < 1.0 |
| <a name="provider_random"></a> [random](#provider\_random) | >= 3.0 |

## Modules

No modules.

## Resources

| Name | Type |
|------|------|
| [azurerm_cognitive_account.this](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/cognitive_account) | resource |
| [azurerm_cognitive_deployment.this](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/cognitive_deployment) | resource |
| [azurerm_monitor_diagnostic_setting.setting](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/monitor_diagnostic_setting) | resource |
| [azurerm_private_dns_zone.dns_zone](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/private_dns_zone) | resource |
| [azurerm_private_dns_zone_virtual_network_link.dns_zone_link](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/private_dns_zone_virtual_network_link) | resource |
| [azurerm_private_endpoint.this](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/private_endpoint) | resource |
| [modtm_telemetry.this](https://registry.terraform.io/providers/Azure/modtm/latest/docs/resources/telemetry) | resource |
| [random_integer.this](https://registry.terraform.io/providers/hashicorp/random/latest/docs/resources/integer) | resource |
| [azurerm_private_dns_zone.dns_zone](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/data-sources/private_dns_zone) | data source |
| [azurerm_resource_group.pe_vnet_rg](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/data-sources/resource_group) | data source |
| [azurerm_resource_group.this](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/data-sources/resource_group) | data source |
| [azurerm_subnet.pe_subnet](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/data-sources/subnet) | data source |
| [azurerm_virtual_network.vnet](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/data-sources/virtual_network) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_account_name"></a> [account\_name](#input\_account\_name) | Specifies the name of the Cognitive Service Account. Changing this forces a new resource to be created. Leave this variable as default would use a default name with random suffix. | `string` | `""` | no |
| <a name="input_application_name"></a> [application\_name](#input\_application\_name) | Name of the application. A corresponding tag would be created on the created resources if `var.default_tags_enabled` is `true`. | `string` | `""` | no |
| <a name="input_custom_subdomain_name"></a> [custom\_subdomain\_name](#input\_custom\_subdomain\_name) | The subdomain name used for token-based authentication. Changing this forces a new resource to be created. Leave this variable as default would use a default name with random suffix. | `string` | `""` | no |
| <a name="input_customer_managed_key"></a> [customer\_managed\_key](#input\_customer\_managed\_key) | type = object({<br>  key\_vault\_key\_id   = (Required) The ID of the Key Vault Key which should be used to Encrypt the data in this OpenAI Account.<br>  identity\_client\_id = (Optional) The Client ID of the User Assigned Identity that has access to the key. This property only needs to be specified when there're multiple identities attached to the OpenAI Account.<br>}) | <pre>object({<br>    key_vault_key_id   = string<br>    identity_client_id = optional(string)<br>  })</pre> | `null` | no |
| <a name="input_default_tags_enabled"></a> [default\_tags\_enabled](#input\_default\_tags\_enabled) | Determines whether or not default tags are applied to resources. If set to true, tags will be applied. If set to false, tags will not be applied. | `bool` | `false` | no |
| <a name="input_deployment"></a> [deployment](#input\_deployment) | type = map(object({<br>  name                 = (Required) The name of the Cognitive Services Account Deployment. Changing this forces a new resource to be created.<br>  cognitive\_account\_id = (Required) The ID of the Cognitive Services Account. Changing this forces a new resource to be created.<br>  model = {<br>    model\_format  = (Required) The format of the Cognitive Services Account Deployment model. Changing this forces a new resource to be created. Possible value is OpenAI.<br>    model\_name    = (Required) The name of the Cognitive Services Account Deployment model. Changing this forces a new resource to be created.<br>    model\_version = (Required) The version of Cognitive Services Account Deployment model.<br>  }<br>  scale = {<br>    scale\_type = (Required) Deployment scale type. Possible value is Standard. Changing this forces a new resource to be created.<br>  }<br>  rai\_policy\_name = (Optional) The name of RAI policy. Changing this forces a new resource to be created.<br>  capacity = (Optional) Tokens-per-Minute (TPM). The unit of measure for this field is in the thousands of Tokens-per-Minute. Defaults to 1 which means that the limitation is 1000 tokens per minute.<br>  version\_upgrade\_option = (Optional) Deployment model version upgrade option. Possible values are `OnceNewDefaultVersionAvailable`, `OnceCurrentVersionExpired`, and `NoAutoUpgrade`. Defaults to `OnceNewDefaultVersionAvailable`. Changing this forces a new resource to be created.<br>})) | <pre>map(object({<br>    name                   = string<br>    model_format           = string<br>    model_name             = string<br>    model_version          = string<br>    scale_type             = string<br>    rai_policy_name        = optional(string)<br>    capacity               = optional(number)<br>    version_upgrade_option = optional(string)<br>  }))</pre> | `{}` | no |
| <a name="input_diagnostic_setting"></a> [diagnostic\_setting](#input\_diagnostic\_setting) | A map of objects that represent the configuration for a diagnostic setting."<br>type = map(object({<br>  name                                  = (Required) Specifies the name of the diagnostic setting. Changing this forces a new resource to be created.<br>  log\_analytics\_workspace\_id            = (Optional) (Optional) Specifies the resource id of an Azure Log Analytics workspace where diagnostics data should be sent.<br>  log\_analytics\_destination\_type        = (Optional) Possible values are `AzureDiagnostics` and `Dedicated`. When set to Dedicated, logs sent to a Log Analytics workspace will go into resource specific tables, instead of the legacy `AzureDiagnostics` table.<br>  eventhub\_name                         = (Optional) Specifies the name of the Event Hub where diagnostics data should be sent.<br>  eventhub\_authorization\_rule\_id        = (Optional) Specifies the resource id of an Event Hub Namespace Authorization Rule used to send diagnostics data.<br>  storage\_account\_id                    = (Optional) Specifies the resource id of an Azure storage account where diagnostics data should be sent.<br>  partner\_solution\_id                   = (Optional) The resource id of the market partner solution where diagnostics data should be sent. For potential partner integrations, click to learn more about partner integration.<br>  audit\_log\_retention\_policy            = (Optional) Specifies the retention policy for the audit log. This is a block with the following properties:<br>    enabled                             = (Optional) Specifies whether the retention policy is enabled. If enabled, `days` must be a positive number.<br>    days                                = (Optional) Specifies the number of days to retain trace logs. If `enabled` is set to `true`, this value must be set to a positive number.<br>  request\_response\_log\_retention\_policy = (Optional) Specifies the retention policy for the request response log. This is a block with the following properties:<br>    enabled                             = (Optional) Specifies whether the retention policy is enabled. If enabled, `days` must be a positive number.<br>    days                                = (Optional) Specifies the number of days to retain trace logs. If `enabled` is set to `true`, this value must be set to a positive number.<br>  trace\_log\_retention\_policy            = (Optional) Specifies the retention policy for the trace log. This is a block with the following properties:<br>    enabled                             = (Optional) Specifies whether the retention policy is enabled. If enabled, `days` must be a positive number.<br>    days                                = (Optional) Specifies the number of days to retain trace logs. If `enabled` is set to `true`, this value must be set to a positive number.<br>  metric\_retention\_policy               = (Optional) Specifies the retention policy for the metric. This is a block with the following properties:<br>    enabled                             = (Optional) Specifies whether the retention policy is enabled. If enabled, `days` must be a positive number.<br>    days                                = (Optional) Specifies the number of days to retain trace logs. If `enabled` is set to `true`, this value must be set to a positive number.<br>})) | <pre>map(object({<br>    name                           = string<br>    log_analytics_workspace_id     = optional(string)<br>    log_analytics_destination_type = optional(string)<br>    eventhub_name                  = optional(string)<br>    eventhub_authorization_rule_id = optional(string)<br>    storage_account_id             = optional(string)<br>    partner_solution_id            = optional(string)<br>    audit_log_retention_policy = optional(object({<br>      enabled = optional(bool, true)<br>      days    = optional(number, 7)<br>    }))<br>    request_response_log_retention_policy = optional(object({<br>      enabled = optional(bool, true)<br>      days    = optional(number, 7)<br>    }))<br>    trace_log_retention_policy = optional(object({<br>      enabled = optional(bool, true)<br>      days    = optional(number, 7)<br>    }))<br>    metric_retention_policy = optional(object({<br>      enabled = optional(bool, true)<br>      days    = optional(number, 7)<br>    }))<br>  }))</pre> | `{}` | no |
| <a name="input_dynamic_throttling_enabled"></a> [dynamic\_throttling\_enabled](#input\_dynamic\_throttling\_enabled) | Determines whether or not dynamic throttling is enabled. If set to `true`, dynamic throttling will be enabled. If set to `false`, dynamic throttling will not be enabled. | `bool` | `null` | no |
| <a name="input_environment"></a> [environment](#input\_environment) | Environment of the application. A corresponding tag would be created on the created resources if `var.default_tags_enabled` is `true`. | `string` | `""` | no |
| <a name="input_fqdns"></a> [fqdns](#input\_fqdns) | List of FQDNs allowed for the Cognitive Account. | `list(string)` | `null` | no |
| <a name="input_identity"></a> [identity](#input\_identity) | type = object({<br>  type         = (Required) The type of the Identity. Possible values are `SystemAssigned`, `UserAssigned`, `SystemAssigned, UserAssigned`.<br>  identity\_ids = (Optional) Specifies a list of User Assigned Managed Identity IDs to be assigned to this OpenAI Account.<br>}) | <pre>object({<br>    type         = string<br>    identity_ids = optional(list(string))<br>  })</pre> | `null` | no |
| <a name="input_local_auth_enabled"></a> [local\_auth\_enabled](#input\_local\_auth\_enabled) | Whether local authentication methods is enabled for the Cognitive Account. Defaults to `true`. | `bool` | `true` | no |
| <a name="input_location"></a> [location](#input\_location) | Azure OpenAI deployment region. Set this variable to `null` would use resource group's location. | `string` | n/a | yes |
| <a name="input_network_acls"></a> [network\_acls](#input\_network\_acls) | type = set(object({<br>  default\_action = (Required) The Default Action to use when no rules match from ip\_rules / virtual\_network\_rules. Possible values are `Allow` and `Deny`.<br>  ip\_rules                    = (Optional) One or more IP Addresses, or CIDR Blocks which should be able to access the Cognitive Account.<br>  virtual\_network\_rules = optional(set(object({<br>    subnet\_id                            = (Required) The ID of a Subnet which should be able to access the OpenAI Account.<br>    ignore\_missing\_vnet\_service\_endpoint = (Optional) Whether ignore missing vnet service endpoint or not. Default to `false`.<br>  })))<br>})) | <pre>set(object({<br>    default_action = string<br>    ip_rules       = optional(set(string))<br>    virtual_network_rules = optional(set(object({<br>      subnet_id                            = string<br>      ignore_missing_vnet_service_endpoint = optional(bool, false)<br>    })))<br>  }))</pre> | `null` | no |
| <a name="input_outbound_network_access_restricted"></a> [outbound\_network\_access\_restricted](#input\_outbound\_network\_access\_restricted) | Whether outbound network access is restricted for the Cognitive Account. Defaults to `false`. | `bool` | `false` | no |
| <a name="input_pe_subresource"></a> [pe\_subresource](#input\_pe\_subresource) | A list of subresource names which the Private Endpoint is able to connect to. `subresource_names` corresponds to `group_id`. Possible values are detailed in the product [documentation](https://docs.microsoft.com/azure/private-link/private-endpoint-overview#private-link-resource) in the `Subresources` column. Changing this forces a new resource to be created. | `list(string)` | <pre>[<br>  "account"<br>]</pre> | no |
| <a name="input_private_dns_zone"></a> [private\_dns\_zone](#input\_private\_dns\_zone) | A map of object that represents the existing Private DNS Zone you'd like to use. Leave this variable as default would create a new Private DNS Zone.<br>type = object({<br>  name                = "(Required) The name of the Private DNS Zone."<br>  resource\_group\_name = "(Optional) The Name of the Resource Group where the Private DNS Zone exists. If the Name of the Resource Group is not provided, the first Private DNS Zone from the list of Private DNS Zones in your subscription that matches `name` will be returned."<br>} | <pre>object({<br>    name                = string<br>    resource_group_name = optional(string)<br>  })</pre> | `null` | no |
| <a name="input_private_endpoint"></a> [private\_endpoint](#input\_private\_endpoint) | A map of objects that represent the configuration for a private endpoint."<br>type = map(object({<br>  name                               = (Required) Specifies the Name of the Private Endpoint. Changing this forces a new resource to be created.<br>  vnet\_rg\_name                       = (Required) Specifies the name of the Resource Group where the Private Endpoint's Virtual Network Subnet exists. Changing this forces a new resource to be created.<br>  vnet\_name                          = (Required) Specifies the name of the Virtual Network where the Private Endpoint's Subnet exists. Changing this forces a new resource to be created.<br>  subnet\_name                        = (Required) Specifies the name of the Subnet which Private IP Addresses will be allocated for this Private Endpoint. Changing this forces a new resource to be created.<br>  dns\_zone\_virtual\_network\_link\_name = (Optional) The name of the Private DNS Zone Virtual Network Link. Changing this forces a new resource to be created. Default to `dns_zone_link`.<br>  private\_dns\_entry\_enabled          = (Optional) Whether or not to create a `private_dns_zone_group` block for the Private Endpoint. Default to `false`.<br>  private\_service\_connection\_name    = (Optional) Specifies the Name of the Private Service Connection. Changing this forces a new resource to be created. Default to `privateserviceconnection`.<br>  is\_manual\_connection               = (Optional) Does the Private Endpoint require Manual Approval from the remote resource owner? Changing this forces a new resource to be created. Default to `false`.<br>})) | <pre>map(object({<br>    name                               = string<br>    vnet_rg_name                       = string<br>    vnet_name                          = string<br>    subnet_name                        = string<br>    location                           = optional(string, null)<br>    dns_zone_virtual_network_link_name = optional(string, "dns_zone_link")<br>    private_dns_entry_enabled          = optional(bool, false)<br>    private_service_connection_name    = optional(string, "privateserviceconnection")<br>    is_manual_connection               = optional(bool, false)<br>  }))</pre> | `{}` | no |
| <a name="input_public_network_access_enabled"></a> [public\_network\_access\_enabled](#input\_public\_network\_access\_enabled) | Whether public network access is allowed for the Cognitive Account. Defaults to `false`. | `bool` | `false` | no |
| <a name="input_resource_group_name"></a> [resource\_group\_name](#input\_resource\_group\_name) | Name of the azure resource group to use. The resource group must exist. | `string` | n/a | yes |
| <a name="input_sku_name"></a> [sku\_name](#input\_sku\_name) | Specifies the SKU Name for this Cognitive Service Account. Possible values are `F0`, `F1`, `S0`, `S`, `S1`, `S2`, `S3`, `S4`, `S5`, `S6`, `P0`, `P1`, `P2`, `E0` and `DC0`. Default to `S0`. | `string` | `"S0"` | no |
| <a name="input_tags"></a> [tags](#input\_tags) | (Optional) A mapping of tags to assign to the resource. | `map(string)` | `{}` | no |
| <a name="input_tracing_tags_enabled"></a> [tracing\_tags\_enabled](#input\_tracing\_tags\_enabled) | Whether enable tracing tags that generated by BridgeCrew Yor. | `bool` | `false` | no |
| <a name="input_tracing_tags_prefix"></a> [tracing\_tags\_prefix](#input\_tracing\_tags\_prefix) | Default prefix for generated tracing tags | `string` | `"avm_"` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_openai_endpoint"></a> [openai\_endpoint](#output\_openai\_endpoint) | The endpoint used to connect to the Cognitive Service Account. |
| <a name="output_openai_id"></a> [openai\_id](#output\_openai\_id) | The ID of the Cognitive Service Account. |
| <a name="output_openai_primary_key"></a> [openai\_primary\_key](#output\_openai\_primary\_key) | The primary access key for the Cognitive Service Account. |
| <a name="output_openai_secondary_key"></a> [openai\_secondary\_key](#output\_openai\_secondary\_key) | The secondary access key for the Cognitive Service Account. |
| <a name="output_openai_subdomain"></a> [openai\_subdomain](#output\_openai\_subdomain) | The subdomain used to connect to the Cognitive Service Account. |
| <a name="output_private_ip_addresses"></a> [private\_ip\_addresses](#output\_private\_ip\_addresses) | A map dictionary of the private IP addresses for each private endpoint. |
<!-- END_TF_DOCS -->


# Contributing

Before submitting a pull request, please make sure the following is done:

We provide a docker image to run the pre-commit checks and tests for you: `mcr.microsoft.com/azterraform:latest`

To run the pre-commit task, we can run the following command:

```shell
docker run --rm -v $(pwd):/src -w /src mcr.microsoft.com/azterraform:latest make pre-commit
```

On Windows Powershell:

```shell
docker run --rm -v ${pwd}:/src -w /src mcr.microsoft.com/azterraform:latest make pre-commit
```

In pre-commit task, we will:

1. Run `terraform fmt -recursive` command for your Terraform code.
2. Run `terrafmt fmt -f` command for markdown files and go code files to ensure that the Terraform code embedded in these files are well formatted.
3. Run `go mod tidy` and `go mod vendor` for test folder to ensure that all the dependencies have been synced.
4. Run `gofmt` for all go code files.
5. Run `gofumpt` for all go code files.
6. Run `terraform-docs` on `README.md` file, then run `markdown-table-formatter` to format markdown tables in `README.md`.

Then we can run the pr-check task to check whether our code meets our pipeline's requirement (We strongly recommend you run the following command before you commit):

```shell
docker run --rm -v $(pwd):/src -w /src mcr.microsoft.com/azterraform:latest make pr-check
```

On Windows Powershell:

```shell
docker run --rm -v ${pwd}:/src -w /src mcr.microsoft.com/azterraform:latest make pr-check
```

To run the e2e-test, we can run the following command:

```text
docker run --rm -v $(pwd):/src -w /src -e ARM_SUBSCRIPTION_ID -e ARM_TENANT_ID -e ARM_CLIENT_ID -e ARM_CLIENT_SECRET mcr.microsoft.com/azterraform:latest make e2e-test
```

On Windows Powershell:

```text
docker run --rm -v ${pwd}:/src -w /src -e ARM_SUBSCRIPTION_ID -e ARM_TENANT_ID -e ARM_CLIENT_ID -e ARM_CLIENT_SECRET mcr.microsoft.com/azterraform:latest make e2e-test
```

## Enable or disable tracing tags

We're using [BridgeCrew Yor](https://github.com/bridgecrewio/yor) and [yorbox](https://github.com/lonegunmanb/yorbox) to help manage tags consistently across infrastructure as code (IaC) frameworks. In this module you might see tags like:

```hcl
resource "azurerm_resource_group" "rg" {
  location = "eastus"
  name     = random_pet.name
  tags = merge(var.tags, (/*<box>*/ (var.tracing_tags_enabled ? { for k, v in /*</box>*/ {
    avm_git_commit           = "3077cc6d0b70e29b6e106b3ab98cee6740c916f6"
    avm_git_file             = "main.tf"
    avm_git_last_modified_at = "2023-05-05 08:57:54"
    avm_git_org              = "lonegunmanb"
    avm_git_repo             = "terraform-yor-tag-test-module"
    avm_yor_trace            = "a0425718-c57d-401c-a7d5-f3d88b2551a4"
  } /*<box>*/ : replace(k, "avm_", var.tracing_tags_prefix) => v } : {}) /*</box>*/))
}
```

To enable tracing tags, set the variable to true:

```hcl
module "example" {
  source               = "{module_source}"
  ...
  tracing_tags_enabled = true
}
```

The `tracing_tags_enabled` is default to `false`.

To customize the prefix for your tracing tags, set the `tracing_tags_prefix` variable value in your Terraform configuration:

```hcl
module "example" {
  source              = "{module_source}"
  ...
  tracing_tags_prefix = "custom_prefix_"
}
```

The actual applied tags would be:

```text
{
  custom_prefix_git_commit           = "3077cc6d0b70e29b6e106b3ab98cee6740c916f6"
  custom_prefix_git_file             = "main.tf"
  custom_prefix_git_last_modified_at = "2023-05-05 08:57:54"
  custom_prefix_git_org              = "lonegunmanb"
  custom_prefix_git_repo             = "terraform-yor-tag-test-module"
  custom_prefix_yor_trace            = "a0425718-c57d-401c-a7d5-f3d88b2551a4"
}
```

## Telemetry Collection

This module uses [terraform-provider-modtm](https://registry.terraform.io/providers/Azure/modtm/latest) to collect telemetry data. This provider is designed to assist with tracking the usage of Terraform modules. It creates a custom `modtm_telemetry` resource that gathers and sends telemetry data to a specified endpoint. The aim is to provide visibility into the lifecycle of your Terraform modules - whether they are being created, updated, or deleted. This data can be invaluable in understanding the usage patterns of your modules, identifying popular modules, and recognizing those that are no longer in use.

The ModTM provider is designed with respect for data privacy and control. The only data collected and transmitted are the tags you define in module's `modtm_telemetry` resource, an uuid which represents a module instance's identifier, and the operation the module's caller is executing (Create/Update/Delete/Read). No other data from your Terraform modules or your environment is collected or transmitted.

One of the primary design principles of the ModTM provider is its non-blocking nature. The provider is designed to work in a way that any network disconnectedness or errors during the telemetry data sending process will not cause a Terraform error or interrupt your Terraform operations. This makes the ModTM provider safe to use even in network-restricted or air-gaped environments.

If the telemetry data cannot be sent due to network issues, the failure will be logged, but it will not affect the Terraform operation in progress(it might delay your operations for no more than 5 seconds). This ensures that your Terraform operations always run smoothly and without interruptions, regardless of the network conditions.

You can turn off the telemetry collection by declaring the following `provider` block in your root module:

```hcl
provider "modtm" {
  enabled = false
}
```
