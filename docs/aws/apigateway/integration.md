# API Gateway Integration

Configure backend integrations for API methods using ytofu YAML.

## Lambda Integration

```yaml
resource:
  aws_api_gateway_integration:
    lambda:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      resource_id: ${aws_api_gateway_resource.example.id}
      http_method: ${aws_api_gateway_method.example.http_method}
      integration_http_method: POST
      type: AWS_PROXY
      uri: ${aws_lambda_function.example.invoke_arn}
```

## HTTP Proxy

```yaml
resource:
  aws_api_gateway_integration:
    http:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      resource_id: ${aws_api_gateway_resource.example.id}
      http_method: ${aws_api_gateway_method.example.http_method}
      integration_http_method: GET
      type: HTTP_PROXY
      uri: https://api.example.com/resource
```

## Mock Integration

```yaml
resource:
  aws_api_gateway_integration:
    mock:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      resource_id: ${aws_api_gateway_resource.example.id}
      http_method: ${aws_api_gateway_method.example.http_method}
      type: MOCK
      request_templates:
        application/json: '{"statusCode": 200}'

  aws_api_gateway_integration_response:
    mock:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      resource_id: ${aws_api_gateway_resource.example.id}
      http_method: ${aws_api_gateway_method.example.http_method}
      status_code: ${aws_api_gateway_method_response.ok.status_code}
```

## VPC Link Integration

```yaml
resource:
  aws_api_gateway_integration:
    vpc:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      resource_id: ${aws_api_gateway_resource.example.id}
      http_method: ${aws_api_gateway_method.example.http_method}
      integration_http_method: GET
      type: HTTP_PROXY
      uri: http://${aws_lb.example.dns_name}/api
      connection_type: VPC_LINK
      connection_id: ${aws_api_gateway_vpc_link.example.id}
```
