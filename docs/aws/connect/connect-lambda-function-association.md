# Connect Lambda Function Association

Manage Connect Lambda Function Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_connect_lambda_function_association:
    example:
      function_arn: ${aws_lambda_function.example.arn}
      instance_id: ${aws_connect_instance.example.id}
```
