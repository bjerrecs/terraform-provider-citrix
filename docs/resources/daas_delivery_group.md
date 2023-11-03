---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "citrix_daas_delivery_group Resource - citrix"
subcategory: ""
description: |-
  Manages a delivery group.
---

# citrix_daas_delivery_group (Resource)

Manages a delivery group.

## Example Usage

```terraform
resource "citrix_daas_delivery_group" "example-delivery-group" {
    name = "example-delivery-group"
    associated_machine_catalogs = [
        {
        machine_catalog = citrix_daas_machine_catalog.example-machine-catalog.id
        count = 1
        }
    ]
    autoscale_enabled = true 
    users = [
        "user@example.com",
    ]
    autoscale_settings = {
        disconnect_peak_idle_session_after_seconds = 3600
        log_off_peak_disconnected_session_after_seconds = 3600
        peak_log_off_action = "Nothing"
        power_time_schemes = [
            {
                days_of_week = [
                    "Monday",
                    "Tuesday",
                    "Wednesday",
                    "Thursday",
                    "Friday"
                ]
                display_name = "weekdays schedule"
                peak_time_ranges = [
                    "09:00-17:00"
                ]
                pool_size_schedules = [
                    {
                        "time_range": "00:00-00:00",
                        "pool_size": 1
                    }
                ],
                pool_using_percentage = false
            },
        ]
    }
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `associated_machine_catalogs` (Attributes List) Machine catalogs from which to assign machines to the newly created delivery group. (see [below for nested schema](#nestedatt--associated_machine_catalogs))
- `name` (String) Name of the delivery group.

### Optional

- `autoscale_enabled` (Boolean) Whether auto-scale is enabled for the delivery group.
- `autoscale_settings` (Attributes) The power management settings governing the machine(s) in the delivery group. (see [below for nested schema](#nestedatt--autoscale_settings))
- `description` (String) Description of the delivery group.
- `users` (List of String) The users and groups who are explicitly granted access to the published desktop.

### Read-Only

- `id` (String) GUID identifier of the delivery group.
- `total_machines` (Number) The total number of machines in the delivery group.

<a id="nestedatt--associated_machine_catalogs"></a>
### Nested Schema for `associated_machine_catalogs`

Required:

- `count` (Number) The number of machines to assign from the machine catalog to the delivery group.
- `machine_catalog` (String) Id of the machine catalog from which to add machines.


<a id="nestedatt--autoscale_settings"></a>
### Nested Schema for `autoscale_settings`

Required:

- `power_time_schemes` (Attributes List) Power management time schemes.  No two schemes for the same delivery group may cover the same day of the week. (see [below for nested schema](#nestedatt--autoscale_settings--power_time_schemes))

Optional:

- `disconnect_off_peak_idle_session_after_seconds` (Number) Specifies the time in seconds after which an idle session belonging to the delivery group is disconnected during off-peak time.
- `disconnect_peak_idle_session_after_seconds` (Number) Specifies the time in seconds after which an idle session belonging to the delivery group is disconnected during peak time.
- `log_off_off_peak_disconnected_session_after_seconds` (Number) Specifies the time in seconds after which a disconnected session belonging to the delivery group is terminated during off peak time.
- `log_off_peak_disconnected_session_after_seconds` (Number) Specifies the time in seconds after which a disconnected session belonging to the delivery group is terminated during peak time.
- `off_peak_buffer_size_percent` (Number) The percentage of machines in the delivery group that should be kept available in an idle state outside peak hours.
- `off_peak_disconnect_action` (String) The action to be performed after a configurable period of a user session disconnecting outside peak hours.
- `off_peak_disconnect_timeout_minutes` (Number) The number of minutes before the configured action should be performed after a user session disconnectts outside peak hours.
- `off_peak_extended_disconnect_action` (String) The action to be performed after a second configurable period of a user session disconnecting outside peak hours.
- `off_peak_extended_disconnect_timeout_minutes` (Number) The number of minutes before the second configured action should be performed after a user session disconnects outside peak hours.
- `off_peak_log_off_action` (String) The action to be performed after a configurable period of a user session ending outside peak hours.
- `peak_buffer_size_percent` (Number) The percentage of machines in the delivery group that should be kept available in an idle state in peak hours.
- `peak_disconnect_action` (String) The action to be performed after a configurable period of a user session disconnecting in peak hours.
- `peak_disconnect_timeout_minutes` (Number) The number of minutes before the configured action should be performed after a user session disconnects in peak hours.
- `peak_extended_disconnect_action` (String) The action to be performed after a second configurable period of a user session disconnecting in peak hours.
- `peak_extended_disconnect_timeout_minutes` (Number) The number of minutes before the second configured action should be performed after a user session disconnects in peak hours.
- `peak_log_off_action` (String) The action to be performed after a configurable period of a user session ending in peak hours.
- `power_off_delay_minutes` (Number) Delay before machines are powered off, when scaling down. Specified in minutes. Applies only to multi-session machines.
- `timezone` (String) The time zone in which this delivery group's machines reside.

<a id="nestedatt--autoscale_settings--power_time_schemes"></a>
### Nested Schema for `autoscale_settings.power_time_schemes`

Required:

- `days_of_week` (List of String) The pattern of days of the week that the power time scheme covers.
- `display_name` (String) The name of the power time scheme as displayed in the console.
- `peak_time_ranges` (List of String) List of peak time ranges during the day. e.g. 09:00-17:00
- `pool_size_schedules` (Attributes List) List of pool size schedules during the day. Each is specified as a time range and an indicator of the number of machines that should be powered on during that time range. (see [below for nested schema](#nestedatt--autoscale_settings--power_time_schemes--pool_size_schedules))
- `pool_using_percentage` (Boolean) Indicates whether the integer values in the pool size array are to be treated as absolute values (if this value is `false`) or as percentages of the number of machines in the delivery group (if this value is `true`).

<a id="nestedatt--autoscale_settings--power_time_schemes--pool_size_schedules"></a>
### Nested Schema for `autoscale_settings.power_time_schemes.pool_size_schedules`

Required:

- `pool_size` (Number) The number of machines (either as an absolute number or a percentage of the machines in the delivery group, depending on the value of PoolUsingPercentage) that are to be maintained in a running state, whether they are in use or not.
- `time_range` (String) Time range during which the pool size applies.

## Import

Import is supported using the following syntax:

```shell
# Delivery Group can be imported by specifying the GUID
terraform import citrix_daas_delivery_group.example-delivery-group a92ac0d6-9a0f-477a-a504-07cae8fccb81
```