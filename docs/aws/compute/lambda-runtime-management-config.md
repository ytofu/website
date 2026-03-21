# Lambda Runtime Management Config

Manage Lambda Runtime Management Config resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lambda_runtime_management_config:
    example:
      function_name: ${aws_lambda_function.example.function_name}
      update_runtime_on: FunctionUpdate
```

## Manual Update

```yaml
resource:
  aws_lambda_runtime_management_config:
    example:
      function_name: ${aws_lambda_function.example.function_name}
      update_runtime_on: Manual
      runtime_version_arn: "arn:aws:lambda:us-east-1::runtime:abcd1234"
```
