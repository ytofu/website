# Lambda Invocation

Manage Lambda Invocation resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lambda_function:
    example:
      filename: function.zip
      function_name: data_processor
      role: ${aws_iam_role.lambda_role.arn}
      handler: index.handler
      runtime: python3.12

resource:
  aws_lambda_invocation:
    example:
      function_name: ${aws_lambda_function.example.function_name}
      input: '{ "operation": "initialize" "config": { "environment": "production" "debug": false } }'

output:
  initialization_result:
    value: ${jsondecode(aws_lambda_invocation.example.result)["status"]}
```

## Dynamic Invocation with Triggers

```yaml
resource:
  aws_lambda_invocation:
    example:
      function_name: ${aws_lambda_function.example.function_name}
      triggers:
        function_version: ${aws_lambda_function.example.version}
        config_hash: example-config-hash
      input: '{ "operation": "process_data" "environment": var.environment "batch_id": random_uuid.batch_id.result }'
```

## CRUD Lifecycle Management

```yaml
resource:
  aws_lambda_invocation:
    example:
      function_name: ${aws_lambda_function.example.function_name}
      input: '{ "resource_name": "database_setup" "database_url": aws_db_instance.example.endpoint "credentials": { "username": var.db_username "password": var.db_password } }'
      lifecycle_scope: CRUD
```
