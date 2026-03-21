# Resource: aws_wafv2_web_acl_association

Creates a WAFv2 Web ACL Association.

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

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `resource_arn` - (Required) The Amazon Resource Name (ARN) of the resource to associate with the web ACL. This must be an ARN of an Application Load Balancer, an Amazon API Gateway stage (REST only, HTTP is unsupported), an Amazon Cognito User Pool, an Amazon AppSync GraphQL API, an Amazon App Runner service, or an Amazon Verified Access instance.
* `web_acl_arn` - (Required) The Amazon Resource Name (ARN) of the Web ACL that you want to associate with the resource.

## Attribute Reference

This resource exports no additional attributes.

## Timeouts

Configuration options:

* `create` - (Default `5m`)

## Import

```bash
ytofu import aws_wafv2_web_acl_association.example arn:aws:wafv2:...7ce849ea,arn:aws:apigateway:...ages/name
```
