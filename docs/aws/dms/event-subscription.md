# DMS Event Subscription

Subscribe to DMS events using ytofu YAML.

## Basic Subscription

```yaml
resource:
  aws_dms_event_subscription:
    example:
      enabled: true
      event_categories:
        - creation
        - failure
      name: example
      sns_topic_arn: ${aws_sns_topic.example.arn}
      source_ids:
        - ${aws_dms_replication_task.example.replication_task_id}
      source_type: replication-task
```
