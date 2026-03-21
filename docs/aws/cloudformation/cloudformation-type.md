# Cloudformation Type

Manage Cloudformation Type resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudformation_type:
    example:
      schema_handler_package: "s3://${aws_s3_object.example.bucket}/${aws_s3_object.example.key}"
      type: RESOURCE
      type_name: "ExampleCompany::ExampleService::ExampleResource"
      logging_config:
        log_group_name: ${aws_cloudwatch_log_group.example.name}
        log_role_arn: ${aws_iam_role.example.arn}
      lifecycle:
        create_before_destroy: true
```
