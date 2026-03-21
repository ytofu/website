# Prometheus Query Logging Configuration

Manage Prometheus Query Logging Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_prometheus_workspace:
    example:
      alias: example

resource:
  aws_cloudwatch_log_group:
    example:
      name: /aws/prometheus/query-logs/example

resource:
  aws_prometheus_query_logging_configuration:
    example:
      workspace_id: ${aws_prometheus_workspace.example.id}
      destination:
        cloudwatch_logs:
          log_group_arn: "${aws_cloudwatch_log_group.example.arn}:*"
        filters:
          qsp_threshold: 1000
```
