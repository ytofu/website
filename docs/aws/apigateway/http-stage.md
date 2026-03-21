# API Gateway v2 Stage

Create deployment stages for HTTP APIs using ytofu YAML.

## Default Stage

```yaml
resource:
  aws_apigatewayv2_stage:
    default:
      api_id: ${aws_apigatewayv2_api.example.id}
      name: $default
      auto_deploy: true
```

## With Logging

```yaml
resource:
  aws_apigatewayv2_stage:
    example:
      api_id: ${aws_apigatewayv2_api.example.id}
      name: prod
      auto_deploy: true
      access_log_settings:
        destination_arn: ${aws_cloudwatch_log_group.example.arn}
        format: $request.id $request.method $request.path $status
      default_route_settings:
        throttling_burst_limit: 100
        throttling_rate_limit: 50
```

## With Stage Variables

```yaml
resource:
  aws_apigatewayv2_stage:
    example:
      api_id: ${aws_apigatewayv2_api.example.id}
      name: prod
      stage_variables:
        env: production
```
