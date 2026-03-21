# Odb Cloud Autonomous Vm Cluster

Manage Odb Cloud Autonomous Vm Cluster resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_odb_cloud_autonomous_vm_cluster:
    avmc_with_minimum_parameters:
      cloud_exadata_infrastructure_id: <aws_odb_cloud_exadata_infrastructure_id>
      odb_network_id: <aws_odb_network_id>
      display_name: my_autonomous_vm_cluster
      autonomous_data_storage_size_in_tbs: 5
      memory_per_oracle_compute_unit_in_gbs: 2
      total_container_databases: 1
      cpu_core_count_per_node: 40
      license_model: LICENSE_INCLUDED
      db_servers: 
        - <my_db_server_id>
      scan_listener_port_tls: 8561
      scan_listener_port_non_tls: 1024
      maintenance_window:
        preference: NO_PREFERENCE

resource:
  aws_odb_cloud_autonomous_vm_cluster:
    avmc_with_all_params:
      description: my first avmc
      time_zone: UTC
      cloud_exadata_infrastructure_id: <aws_odb_cloud_exadata_infrastructure_id>
      odb_network_id: <aws_odb_network_id>
      display_name: my_autonomous_vm_cluster
      autonomous_data_storage_size_in_tbs: 5
      memory_per_oracle_compute_unit_in_gbs: 2
      total_container_databases: 1
      cpu_core_count_per_node: 40
      license_model: LICENSE_INCLUDED
      db_servers: 
        - <my_db_server_1>
        - <my_db_server_2>
      scan_listener_port_tls: 8561
      scan_listener_port_non_tls: 1024
      maintenance_window:
        days_of_week: 
          - name: MONDAY
          - name: TUESDAY
        hours_of_day: 
          - 4
          - 16
        lead_time_in_weeks: 3
        months: 
          - name: FEBRUARY
          - name: MAY
          - name: AUGUST
          - name: NOVEMBER
        preference: CUSTOM_PREFERENCE
        weeks_of_month: 
          - 2
          - 4
      tags: 
```
