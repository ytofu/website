# API Gateway v2 Integration

Configure backend integrations for HTTP APIs using ytofu YAML.

## Lambda Integration

```yaml
resource:
  aws_apigatewayv2_integration:
    example:
      api_id: ${aws_apigatewayv2_api.example.id}
      integration_uri: ${aws_lambda_function.example.invoke_arn}
      integration_type: AWS_PROXY
      payload_format_version: "2.0"
```

## HTTP Proxy

```yaml
resource:
  aws_apigatewayv2_integration:
    example:
      api_id: ${aws_apigatewayv2_api.example.id}
      integration_type: HTTP_PROXY
      integration_method: GET
      integration_uri: https://api.example.com
```

## VPC Link Integration

```yaml
resource:
  aws_apigatewayv2_integration:
    example:
      api_id: ${aws_apigatewayv2_api.example.id}
      integration_type: HTTP_PROXY
      integration_method: ANY
      integration_uri: ${aws_lb_listener.example.arn}
      connection_type: VPC_LINK
      connection_id: ${aws_apigatewayv2_vpc_link.example.id}
```
