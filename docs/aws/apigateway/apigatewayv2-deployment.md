# Resource: aws_apigatewayv2_deployment

Manages an Amazon API Gateway Version 2 deployment.
More information can be found in the [Amazon API Gateway Developer Guide](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-websocket-api.html).

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

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `api_id` - (Required) API identifier.
* `description` - (Optional) Description for the deployment resource. Must be less than or equal to 1024 characters in length.
* `triggers` - (Optional) Map of arbitrary keys and values that, when changed, will trigger a redeployment. To force a redeployment without changing these keys/values, use the `ytofu taint` command.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Deployment identifier.
* `auto_deployed` - Whether the deployment was automatically released.

## Import

```bash
ytofu import aws_apigatewayv2_deployment.example aabbccddee/1122334
```
