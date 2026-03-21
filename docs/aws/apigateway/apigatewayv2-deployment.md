# Apigatewayv2 Deployment

Manage Apigatewayv2 Deployment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_apigatewayv2_deployment:
    example:
      api_id: ${aws_apigatewayv2_api.example.id}
      description: Example deployment
      lifecycle:
        create_before_destroy: true
```

## Redeployment Triggers

```yaml
resource:
  aws_apigatewayv2_deployment:
    example:
      api_id: ${aws_apigatewayv2_api.example.id}
      description: Example deployment
      triggers:
        redeployment: ${sha1(join(",", tolist([ jsonencode(aws_apigatewayv2_integration.example), jsonencode(aws_apigatewayv2_route.example), ])))}
      lifecycle:
        create_before_destroy: true
```
