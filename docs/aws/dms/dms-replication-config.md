# DMS Replication Config

Manage DMS Replication Config resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_dms_replication_config:
    name:
      replication_config_identifier: test-dms-serverless-replication-tf
      resource_identifier: test-dms-serverless-replication-tf
      replication_type: cdc
      source_endpoint_arn: ${aws_dms_endpoint.source.endpoint_arn}
      target_endpoint_arn: ${aws_dms_endpoint.target.endpoint_arn}
      table_mappings: |
        {
        "rules":[{"rule-type":"selection","rule-id":"1","rule-name":"1","rule-action":"include","object-locator":{"schema-name":"%%","table-name":"%%"}}]
        }
      start_replication: true
      compute_config:
        replication_subnet_group_id: ${aws_dms_replication_subnet_group.default.replication_subnet_group_id}
        max_capacity_units: 64
        min_capacity_units: 2
        preferred_maintenance_window: "sun:23:45-mon:00:30"
```
