---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "citrix_azure_hypervisor Resource - citrix"
subcategory: ""
description: |-
  Manages an Azure hypervisor.
---

# citrix_azure_hypervisor (Resource)

Manages an Azure hypervisor.

## Example Usage

```terraform
# Azure Hypervisor
resource "citrix_azure_hypervisor" "example-azure-hypervisor" {
    name                = "example-azure-hypervisor"
    zone                = "<Zone Id>"
    active_directory_id = "<Azure Tenant Id>"
    subscription_id     = "<Azure Subscription Id>"
    application_secret  = "<Azure Client Secret>"
    application_id      = "<Azure Client Id>"
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `active_directory_id` (String) Azure Active Directory ID.
- `application_id` (String) Application ID of the service principal used to access the Azure APIs.
- `application_secret` (String, Sensitive) The Application Secret of the service principal used to access the Azure APIs.
- `name` (String) Name of the hypervisor.
- `subscription_id` (String) Azure Subscription ID.
- `zone` (String) Id of the zone the hypervisor is associated with.

### Optional

- `application_secret_expiration_date` (String) The expiration date of the application secret of the service principal used to access the Azure APIs. Format is YYYY-MM-DD.
- `enable_azure_ad_device_management` (Boolean) Enable Azure AD device management. Default is false.

### Read-Only

- `id` (String) GUID identifier of the hypervisor.

## Import

Import is supported using the following syntax:

```shell
# Azure Hypervisor can be imported by specifying the GUID
terraform import citrix_azure_hypervisor.example-azure-hypervisor b2339edf-7b00-436e-9c3a-54c987c3526e
```