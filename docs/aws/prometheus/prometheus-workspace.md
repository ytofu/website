# Prometheus Workspace

Manage Prometheus Workspace resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_prometheus_workspace:
    example:
      alias: example
      tags:
        Environment: production
```

## CloudWatch Logging

```yaml
resource:
  aws_cloudwatch_log_group:
    example:
      name: example

resource:
  aws_prometheus_workspace:
    example:
      logging_configuration:
        log_group_arn: "${aws_cloudwatch_log_group.example.arn}:*"
```

## AWS KMS Customer Managed Keys (CMK)

```yaml
resource:
  aws_prometheus_workspace:
    example:
      alias: example
      kms_key_arn: ${aws_kms_key.example.arn}

resource:
  aws_kms_key:
    example:
      description: example
      deletion_window_in_days: 7
```
