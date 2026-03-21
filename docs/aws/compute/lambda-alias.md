# Lambda Alias

Manage Lambda Alias resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lambda_alias:
    example:
      name: production
      description: Production environment alias
      function_name: ${aws_lambda_function.example.arn}
      function_version: 1
```

## Alias with Traffic Splitting

```yaml
resource:
  aws_lambda_alias:
    example:
      name: staging
      description: Staging environment with traffic splitting
      function_name: ${aws_lambda_function.example.function_name}
      function_version: 2
      routing_config:
        additional_version_weights: 
```

## Blue-Green Deployment Alias

```yaml
resource:
  aws_lambda_alias:
    example:
      name: live
      description: Live traffic with gradual rollout to new version
      function_name: ${aws_lambda_function.example.function_name}
      function_version: "5" # Current stable version
      routing_config:
        additional_version_weights: 
```

## Development Alias

```yaml
resource:
  aws_lambda_alias:
    example:
      name: dev
      description: Development environment - always points to latest
      function_name: ${aws_lambda_function.example.function_name}
      function_version: $LATEST
```
