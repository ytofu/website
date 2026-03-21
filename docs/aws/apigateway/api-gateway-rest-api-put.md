# API Gateway Rest API Put

Manage API Gateway Rest API Put resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_api_gateway_rest_api_put:
    example:
      body: '{ "swagger": "2.0" "info": { "title": "Example API" "version": "v1" } "schemes": ["https"] "paths": { "/example" = { "get": { "responses": { "200" = { "description": "OK" } } x-amazon-apigateway-"integration": { "httpMethod": "GET" "type": "HTTP" "responses": { "default": { "statusCode": 200 } } "uri": "https://api.example.com/" } } } } }'
      fail_on_warnings: true
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
```

## Multi-stage

```yaml
resource:
  aws_api_gateway_rest_api:
    example:
      name: Example API

resource:
  aws_api_gateway_rest_api_put:
    examplev1:
      body: file-content
      fail_on_warnings: true
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      triggers:
        redeployment: example-value
      lifecycle:
        create_before_destroy: true

resource:
  aws_api_gateway_deployment:
    examplev1:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      triggers:
        redeployment: ${aws_api_gateway_rest_api_put.examplev1.triggers.redeployment}
      lifecycle:
        create_before_destroy: true

resource:
  aws_api_gateway_stage:
    examplev1:
      stage_name: v1
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      deployment_id: ${aws_api_gateway_deployment.examplev1.id}

resource:
  aws_api_gateway_rest_api_put:
    examplev2:
      depends_on:
        - ${aws_api_gateway_stage.examplev1}
      body: file-content
      fail_on_warnings: true
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      triggers:
        redeployment: example-value
      lifecycle:
        create_before_destroy: true

resource:
  aws_api_gateway_deployment:
    examplev2:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      triggers:
        redeployment: ${aws_api_gateway_rest_api_put.examplev2.triggers.redeployment}
      lifecycle:
        create_before_destroy: true

resource:
  aws_api_gateway_stage:
    examplev2:
      stage_name: v2
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      deployment_id: ${aws_api_gateway_deployment.examplev2.id}
```
