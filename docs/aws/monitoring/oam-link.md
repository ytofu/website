# Oam Link

Manage Oam Link resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_oam_link:
    example:
      label_template: $AccountName
      resource_types: 
        - "AWS::CloudWatch::Metric"
      sink_identifier: ${aws_oam_sink.example.arn}
      tags:
        Env: prod
      depends_on:
        - ${aws_oam_sink_policy.example}

resource:
  aws_oam_sink:
    example:

resource:
  aws_oam_sink_policy:
    example:
      sink_identifier: ${aws_oam_sink.example.arn}
```

## Log Group Filtering

```yaml
resource:
  aws_oam_link:
    example:
      label_template: $AccountName
      link_configuration:
        log_group_configuration:
          filter: "LogGroupName LIKE 'aws/lambda/%' OR LogGroupName LIKE 'AWSLogs%'"
      resource_types: 
        - "AWS::Logs::LogGroup"
      sink_identifier: ${aws_oam_sink.example.arn}
      depends_on:
        - ${aws_oam_sink_policy.example}
```

## Metric Filtering

```yaml
resource:
  aws_oam_link:
    example:
      label_template: $AccountName
      link_configuration:
        metric_configuration:
          filter: "Namespace IN ('AWS/EC2', 'AWS/ELB', 'AWS/S3')"
      resource_types: 
        - "AWS::CloudWatch::Metric"
      sink_identifier: ${aws_oam_sink.example.arn}
      depends_on:
        - ${aws_oam_sink_policy.example}
```
