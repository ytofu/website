# Odb Cloud Exadata Infrastructure

Manage Odb Cloud Exadata Infrastructure resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_odb_cloud_exadata_infrastructure:
    example:
      display_name: my-exa-infra
      shape: Exadata.X11M
      storage_count: 3
      compute_count: 2
      availability_zone_id: use1-az6
      customer_contacts_to_send_to_oci: 
        - email: abc@example.com
        - email: def@example.com
      database_server_type: X11M
      storage_server_type: X11M-HC
      maintenance_window:
        custom_action_timeout_in_mins: 16
        days_of_week: 
          - name: MONDAY
          - name: TUESDAY
        hours_of_day: 
          - 11
          - 16
        is_custom_action_timeout_enabled: true
        lead_time_in_weeks: 3
        months: 
          - name: FEBRUARY
          - name: MAY
          - name: AUGUST
          - name: NOVEMBER
        patching_mode: ROLLING
        preference: CUSTOM_PREFERENCE
        weeks_of_month: 
          - 2
          - 4
      tags: 

resource:
  aws_odb_cloud_exadata_infrastructure:
    example:
      display_name: my_exa_X9M
      shape: Exadata.X9M
      storage_count: 3
      compute_count: 2
      availability_zone_id: use1-az6
      maintenance_window:
        custom_action_timeout_in_mins: 16
        is_custom_action_timeout_enabled: true
        patching_mode: ROLLING
        preference: NO_PREFERENCE
```
