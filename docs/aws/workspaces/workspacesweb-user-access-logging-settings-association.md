# Workspacesweb User Access Logging Settings Association

Manage Workspacesweb User Access Logging Settings Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_workspacesweb_portal:
    example:
      display_name: example

resource:
  aws_kinesis_stream:
    example:
      name: amazon-workspaces-web-example
      shard_count: 1

resource:
  aws_workspacesweb_user_access_logging_settings:
    example:
      kinesis_stream_arn: ${aws_kinesis_stream.example.arn}

resource:
  aws_workspacesweb_user_access_logging_settings_association:
    example:
      user_access_logging_settings_arn: ${aws_workspacesweb_user_access_logging_settings.example.user_access_logging_settings_arn}
      portal_arn: ${aws_workspacesweb_portal.example.portal_arn}
```
