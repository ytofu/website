# Lambda Function Recursion Config

Manage Lambda Function Recursion Config resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lambda_function:
    example:
      filename: function.zip
      function_name: recursive_processor
      role: ${aws_iam_role.lambda_role.arn}
      handler: index.handler
      runtime: python3.12

resource:
  aws_lambda_function_recursion_config:
    example:
      function_name: ${aws_lambda_function.example.function_name}
      recursive_loop: Allow
```

## Production Safety Configuration

```yaml
resource:
  aws_lambda_function:
    production_processor:
      filename: processor.zip
      function_name: production-data-processor
      role: ${aws_iam_role.lambda_role.arn}
      handler: app.handler
      runtime: nodejs20.x
      tags:
        Environment: production
        Purpose: data-processing

resource:
  aws_lambda_function_recursion_config:
    example:
      function_name: ${aws_lambda_function.production_processor.function_name}
      recursive_loop: "Terminate" # Safety first in production
```
