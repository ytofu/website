# DMS Replication Task

Create database migration tasks using ytofu YAML.

## Full Load Migration

```yaml
resource:
  aws_dms_replication_task:
    example:
      migration_type: full-load
      replication_instance_arn: ${aws_dms_replication_instance.example.replication_instance_arn}
      replication_task_id: example
      source_endpoint_arn: ${aws_dms_endpoint.source.endpoint_arn}
      target_endpoint_arn: ${aws_dms_endpoint.target.endpoint_arn}
      table_mappings: |
        {
          "rules": [
            {
              "rule-type": "selection",
              "rule-id": "1",
              "rule-name": "1",
              "object-locator": {
                "schema-name": "%",
                "table-name": "%"
              },
              "rule-action": "include"
            }
          ]
        }
```

## CDC (Change Data Capture)

```yaml
resource:
  aws_dms_replication_task:
    cdc:
      migration_type: cdc
      replication_instance_arn: ${aws_dms_replication_instance.example.replication_instance_arn}
      replication_task_id: cdc-task
      source_endpoint_arn: ${aws_dms_endpoint.source.endpoint_arn}
      target_endpoint_arn: ${aws_dms_endpoint.target.endpoint_arn}
      cdc_start_time: "2027-01-01T00:00:00Z"
      table_mappings: |
        {
          "rules": [{"rule-type": "selection", "rule-id": "1", "rule-name": "1", "object-locator": {"schema-name": "public", "table-name": "%"}, "rule-action": "include"}]
        }
```
