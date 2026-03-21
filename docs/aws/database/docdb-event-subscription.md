# Docdb Event Subscription

Manage Docdb Event Subscription resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_docdb_cluster:
    example:
      cluster_identifier: example
      availability_zones: 
        - ${data.aws_availability_zones.available.names[0]}
        - ${data.aws_availability_zones.available.names[1]}
        - ${data.aws_availability_zones.available.names[2]}
      master_username: foo
      master_password: mustbeeightcharaters
      skip_final_snapshot: true

resource:
  aws_sns_topic:
    example:
      name: example-events

resource:
  aws_docdb_event_subscription:
    example:
      name: example
      enabled: true
      event_categories: 
        - creation
        - failure
      source_type: db-cluster
      source_ids: 
        - ${aws_docdb_cluster.example.id}
      sns_topic_arn: ${aws_sns_topic.example.arn}
```
