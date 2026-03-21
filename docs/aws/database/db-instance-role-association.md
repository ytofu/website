# DB Instance Role Association

Manage DB Instance Role Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_db_instance_role_association:
    example:
      db_instance_identifier: ${aws_db_instance.example.identifier}
      feature_name: S3_INTEGRATION
      role_arn: ${aws_iam_role.example.arn}
      lifecycle:
        replace_triggered_by:
          - ${aws_db_instance.example.id}
```
