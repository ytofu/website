# API Gateway Usage Plan

Manage API Gateway Usage Plan resources using ytofu YAML.

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
    development:
      deployment_id: ${aws_api_gateway_deployment.example.id}
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      stage_name: development

resource:
  aws_api_gateway_stage:
    production:
      deployment_id: ${aws_api_gateway_deployment.example.id}
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      stage_name: production

resource:
  aws_api_gateway_usage_plan:
    example:
      name: my-usage-plan
      description: my description
      product_code: MYCODE
      api_stages:
        api_id: ${aws_api_gateway_rest_api.example.id}
        stage: ${aws_api_gateway_stage.development.stage_name}
      api_stages:
        api_id: ${aws_api_gateway_rest_api.example.id}
        stage: ${aws_api_gateway_stage.production.stage_name}
      quota_settings:
        limit: 20
        offset: 2
        period: WEEK
      throttle_settings:
        burst_limit: 5
        rate_limit: 10
```
