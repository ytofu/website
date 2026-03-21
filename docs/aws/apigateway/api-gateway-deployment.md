# API Gateway Deployment

Manage API Gateway Deployment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_api_gateway_rest_api:
    example:
      body: '{ "openapi": "3.0.1" "info": { "title": "example" "version": "1.0" } "paths": { "/path1" = { "get": { x-amazon-apigateway-"integration": { "httpMethod": "GET" "payloadFormatVersion": "1.0" "type": "HTTP_PROXY" "uri": "https://ip-ranges.amazonaws.com/ip-ranges.json" } } } } }'
      name: example

resource:
  aws_api_gateway_deployment:
    example:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      triggers:
        redeployment: example-value
      lifecycle:
        create_before_destroy: true

resource:
  aws_api_gateway_stage:
    example:
      deployment_id: ${aws_api_gateway_deployment.example.id}
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      stage_name: example
```

## Terraform Resources

```yaml
resource:
  aws_api_gateway_rest_api:
    example:
      name: example

resource:
  aws_api_gateway_resource:
    example:
      parent_id: ${aws_api_gateway_rest_api.example.root_resource_id}
      path_part: example
      rest_api_id: ${aws_api_gateway_rest_api.example.id}

resource:
  aws_api_gateway_method:
    example:
      authorization: NONE
      http_method: GET
      resource_id: ${aws_api_gateway_resource.example.id}
      rest_api_id: ${aws_api_gateway_rest_api.example.id}

resource:
  aws_api_gateway_integration:
    example:
      http_method: ${aws_api_gateway_method.example.http_method}
      resource_id: ${aws_api_gateway_resource.example.id}
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      type: MOCK

resource:
  aws_api_gateway_deployment:
    example:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      triggers:
        redeployment: example-value
      lifecycle:
        create_before_destroy: true

resource:
  aws_api_gateway_stage:
    example:
      deployment_id: ${aws_api_gateway_deployment.example.id}
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      stage_name: example
```
