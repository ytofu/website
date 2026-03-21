# API Gateway Stage

Manage API Gateway Stage resources using ytofu YAML.

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

resource:
  aws_api_gateway_method_settings:
    example:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      stage_name: ${aws_api_gateway_stage.example.stage_name}
      method_path: "*/*"
      settings:
        metrics_enabled: true
        logging_level: INFO
```

## Managing the API Logging CloudWatch Log Group

```yaml
resource:
  aws_api_gateway_rest_api:
    example:

resource:
  aws_api_gateway_stage:
    example:
      depends_on: 
        - ${aws_cloudwatch_log_group.example}
      stage_name: example-stage_name

resource:
  aws_cloudwatch_log_group:
    example:
      name: "API-Gateway-Execution-Logs_${aws_api_gateway_rest_api.example.id}/example-stage_name"
      retention_in_days: 7
```
