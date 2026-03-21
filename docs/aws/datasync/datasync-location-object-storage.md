# Datasync Location Object Storage

Manage Datasync Location Object Storage resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_datasync_location_object_storage:
    example:
      agent_arns: 
        - ${aws_datasync_agent.example.arn}
      server_hostname: example
      bucket_name: example
```
