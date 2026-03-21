# Evidently Project

Manage Evidently Project resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_evidently_project:
    example:
      name: Example
      description: Example Description
      tags: 
```

## Store evaluation events in a CloudWatch Log Group

```yaml
resource:
  aws_evidently_project:
    example:
      name: Example
      description: Example Description
      data_delivery:
        cloudwatch_logs:
          log_group: example-log-group-name
      tags: 
```

## Store evaluation events in an S3 bucket

```yaml
resource:
  aws_evidently_project:
    example:
      name: Example
      description: Example Description
      data_delivery:
        s3_destination:
          bucket: example-bucket-name
          prefix: example
      tags: 
```
