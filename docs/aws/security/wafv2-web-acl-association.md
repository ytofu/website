# Wafv2 Web Acl Association

Manage Wafv2 Web Acl Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_api_gateway_rest_api:
    example:
      body: '{ "openapi": "3.0.1" "info": { "title": "example" "version": "1.0" } "paths": { "/path1" = { "get": { "x-amazon-apigateway-integration" = { "httpMethod": "GET" "payloadFormatVersion": "1.0" "type": "HTTP_PROXY" "uri": "https://ip-ranges.amazonaws.com/ip-ranges.json" } } } } }'
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
  aws_wafv2_web_acl:
    example:
      name: web-acl-association-example
      scope: REGIONAL
      default_action:
        allow:
        visibility_config:
          cloudwatch_metrics_enabled: false
          metric_name: friendly-metric-name
          sampled_requests_enabled: false

resource:
  aws_wafv2_web_acl_association:
    example:
      resource_arn: ${aws_api_gateway_stage.example.arn}
      web_acl_arn: ${aws_wafv2_web_acl.example.arn}
```
