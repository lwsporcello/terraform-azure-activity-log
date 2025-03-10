<a href="https://lacework.com"><img src="https://techally-content.s3-us-west-1.amazonaws.com/public-content/lacework_logo_full.png" width="600"></a>

# terraform-azure-activity-log

[![GitHub release](https://img.shields.io/github/release/lacework/terraform-azure-activity-log.svg)](https://github.com/lacework/terraform-azure-activity-log/releases/)
[![Codefresh build status](https://g.codefresh.io/api/badges/pipeline/lacework/terraform-modules%2Ftest-compatibility?type=cf-1&key=eyJhbGciOiJIUzI1NiJ9.NWVmNTAxOGU4Y2FjOGQzYTkxYjg3ZDEx.RJ3DEzWmBXrJX7m38iExJ_ntGv4_Ip8VTa-an8gBwBo)](https://g.codefresh.io/pipelines/edit/new/builds?id=607e25e6728f5a6fba30431b&pipeline=test-compatibility&projects=terraform-modules&projectId=607db54b728f5a5f8930405d)

Terraform module for configuring an integration with Azure Subscriptions and Tenants for Activity Log analysis.
It configures a Diagnostic Setting that puts logs in an storage account, from which Lacework will read Activity Logs.

## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 0.14 |
| <a name="requirement_azurerm"></a> [azurerm](#requirement\_azurerm) | ~> 2.28 |
| <a name="requirement_lacework"></a> [lacework](#requirement\_lacework) | ~> 0.3 |
| <a name="requirement_random"></a> [random](#requirement\_random) | >= 2.1 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_azurerm"></a> [azurerm](#provider\_azurerm) | ~> 2.28 |
| <a name="provider_lacework"></a> [lacework](#provider\_lacework) | ~> 0.3 |
| <a name="provider_random"></a> [random](#provider\_random) | >= 2.1 |
| <a name="provider_time"></a> [time](#provider\_time) | n/a |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_az_ad_application"></a> [az\_ad\_application](#module\_az\_ad\_application) | lacework/ad-application/azure | ~> 1.0 |

## Resources

| Name | Type |
|------|------|
| [azurerm_eventgrid_event_subscription.lacework](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/eventgrid_event_subscription) | resource |
| [azurerm_monitor_diagnostic_setting.lacework](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/monitor_diagnostic_setting) | resource |
| [azurerm_resource_group.lacework](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/resource_group) | resource |
| [azurerm_role_assignment.lacework](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/role_assignment) | resource |
| [azurerm_role_definition.lacework](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/role_definition) | resource |
| [azurerm_storage_account.lacework](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/storage_account) | resource |
| [azurerm_storage_queue.lacework](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/storage_queue) | resource |
| [lacework_integration_azure_al.lacework](https://registry.terraform.io/providers/lacework/lacework/latest/docs/resources/integration_azure_al) | resource |
| [random_id.uniq](https://registry.terraform.io/providers/hashicorp/random/latest/docs/resources/id) | resource |
| [time_sleep.wait_time](https://registry.terraform.io/providers/hashicorp/time/latest/docs/resources/sleep) | resource |
| [azurerm_storage_account.lacework](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/data-sources/storage_account) | data source |
| [azurerm_subscription.primary](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/data-sources/subscription) | data source |
| [azurerm_subscriptions.available](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/data-sources/subscriptions) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_all_subscriptions"></a> [all\_subscriptions](#input\_all\_subscriptions) | If set to `true`, grant read access to ALL subscriptions within the selected Tenant (overrides `subscription_ids`) | `bool` | `false` | no |
| <a name="input_application_id"></a> [application\_id](#input\_application\_id) | The Active Directory Application id to use (required when use\_existing\_ad\_application is set to true) | `string` | `""` | no |
| <a name="input_application_name"></a> [application\_name](#input\_application\_name) | The name of the Azure Active Directory Application (required when use\_existing\_ad\_application is set to true) | `string` | `"lacework_security_audit"` | no |
| <a name="input_application_password"></a> [application\_password](#input\_application\_password) | The Active Directory Application password to use (required when use\_existing\_ad\_application is set to true) | `string` | `""` | no |
| <a name="input_diagnostic_settings_name"></a> [diagnostic\_settings\_name](#input\_diagnostic\_settings\_name) | The name of the subscription's Diagnostic Setting for Activity Logs | `string` | `"lacework_activity_logs"` | no |
| <a name="input_lacework_integration_name"></a> [lacework\_integration\_name](#input\_lacework\_integration\_name) | The Lacework integration name | `string` | `"TF activity log"` | no |
| <a name="input_location"></a> [location](#input\_location) | Azure region where the storage account for logging will reside | `string` | `"West US 2"` | no |
| <a name="input_prefix"></a> [prefix](#input\_prefix) | The prefix to use at the beginning of every generated resource | `string` | `"lacework"` | no |
| <a name="input_service_principal_id"></a> [service\_principal\_id](#input\_service\_principal\_id) | The Enterprise App Object ID related to the application\_id (required when use\_existing\_ad\_application is true) | `string` | `""` | no |
| <a name="input_storage_account_name"></a> [storage\_account\_name](#input\_storage\_account\_name) | The name of the Storage Account | `string` | `""` | no |
| <a name="input_storage_account_resource_group"></a> [storage\_account\_resource\_group](#input\_storage\_account\_resource\_group) | The Resource Group for the existing Storage Account | `string` | `""` | no |
| <a name="input_subscription_ids"></a> [subscription\_ids](#input\_subscription\_ids) | List of subscriptions to enable logging (by default the module will only use the primary subscription) | `list(string)` | `[]` | no |
| <a name="input_tags"></a> [tags](#input\_tags) | Key-value map of Tag names and Tag values | `map(string)` | `{}` | no |
| <a name="input_use_existing_ad_application"></a> [use\_existing\_ad\_application](#input\_use\_existing\_ad\_application) | Set this to `true` to use an existing Active Directory Application | `bool` | `false` | no |
| <a name="input_use_existing_storage_account"></a> [use\_existing\_storage\_account](#input\_use\_existing\_storage\_account) | Set this to `true` to use an existing Storage Account. Default behavior creates a new Storage Account | `bool` | `false` | no |
| <a name="input_wait_time"></a> [wait\_time](#input\_wait\_time) | Amount of time to wait before the Lacework resources are provisioned | `string` | `"50s"` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_application_id"></a> [application\_id](#output\_application\_id) | The Lacework AD Application id |
| <a name="output_application_password"></a> [application\_password](#output\_application\_password) | The Lacework AD Application password |
| <a name="output_diagnostic_settings_name"></a> [diagnostic\_settings\_name](#output\_diagnostic\_settings\_name) | The name of the subscription's Diagnostic Setting for Activity Logs |
| <a name="output_service_principal_id"></a> [service\_principal\_id](#output\_service\_principal\_id) | The Lacework Service Principal id |
| <a name="output_storage_account_name"></a> [storage\_account\_name](#output\_storage\_account\_name) | The name of the centralized Storage Account for Activity Logs |
| <a name="output_storage_account_resource_group"></a> [storage\_account\_resource\_group](#output\_storage\_account\_resource\_group) | The resource group of the centralized Storage Account for Activity Logs |
| <a name="output_subscription_ids"></a> [subscription\_ids](#output\_subscription\_ids) | The list of subscriptions that will send Activity Logs to the storage account |
