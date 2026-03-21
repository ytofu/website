# Workspacesweb User Access Logging Settings

Manage Workspacesweb User Access Logging Settings resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_kinesis_stream:
    example:
      name: amazon-workspaces-web-example-stream
      shard_count: 1

resource:
  aws_workspacesweb_user_access_logging_settings:
    example:
      kinesis_stream_arn: ${aws_kinesis_stream.example.arn}
```

## With Tags

```yaml
resource:
  aws_kinesis_stream:
    example:
      name: example-stream
      shard_count: 1

resource:
  aws_workspacesweb_user_access_logging_settings:
    example:
      kinesis_stream_arn: ${aws_kinesis_stream.example.arn}
      tags:
        Name: example-user-access-logging-settings
        Environment: Production
```
