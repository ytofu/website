# IAM Service Linked Role

Manage IAM Service Linked Role resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iam_service_linked_role:
    elasticbeanstalk:
      aws_service_name: elasticbeanstalk.amazonaws.com
```
