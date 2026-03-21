# Apigatewayv2 Integration

Manage Apigatewayv2 Integration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_apigatewayv2_integration:
    example:
      api_id: ${aws_apigatewayv2_api.example.id}
      integration_type: MOCK
```

## Lambda Integration

```yaml
resource:
  aws_lambda_function:
    example:
      filename: example.zip
      function_name: Example
      role: ${aws_iam_role.example.arn}
      handler: index.handler
      runtime: nodejs20.x

resource:
  aws_apigatewayv2_integration:
    example:
      api_id: ${aws_apigatewayv2_api.example.id}
      integration_type: AWS_PROXY
      connection_type: INTERNET
      content_handling_strategy: CONVERT_TO_TEXT
      description: Lambda example
      integration_method: POST
      integration_uri: ${aws_lambda_function.example.invoke_arn}
      passthrough_behavior: WHEN_NO_MATCH
```

## AWS Service Integration

```yaml
resource:
  aws_apigatewayv2_integration:
    example:
      api_id: ${aws_apigatewayv2_api.example.id}
      credentials_arn: ${aws_iam_role.example.arn}
      description: SQS example
      integration_type: AWS_PROXY
      integration_subtype: SQS-SendMessage
      request_parameters: 
```

## Private Integration

```yaml
resource:
  aws_apigatewayv2_integration:
    example:
      api_id: ${aws_apigatewayv2_api.example.id}
      credentials_arn: ${aws_iam_role.example.arn}
      description: Example with a load balancer
      integration_type: HTTP_PROXY
      integration_uri: ${aws_lb_listener.example.arn}
      integration_method: ANY
      connection_type: VPC_LINK
      connection_id: ${aws_apigatewayv2_vpc_link.example.id}
      tls_config:
        server_name_to_verify: example.com
      request_parameters: 
      response_parameters:
        status_code: 403
        mappings: 
      response_parameters:
        status_code: 200
        mappings: 
```
