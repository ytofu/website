# Lambda Provisioned Concurrency Config

Manage Lambda Provisioned Concurrency Config resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lambda_provisioned_concurrency_config:
    example:
      function_name: ${aws_lambda_alias.example.function_name}
      provisioned_concurrent_executions: 1
      qualifier: ${aws_lambda_alias.example.name}
```

## Function Version

```yaml
resource:
  aws_lambda_provisioned_concurrency_config:
    example:
      function_name: ${aws_lambda_function.example.function_name}
      provisioned_concurrent_executions: 1
      qualifier: ${aws_lambda_function.example.version}
```
