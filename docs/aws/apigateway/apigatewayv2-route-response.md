# Resource: aws_apigatewayv2_route_response

Manages an Amazon API Gateway Version 2 route response.
More information can be found in the [Amazon API Gateway Developer Guide](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-websocket-api.html).

## Basic Example

```yaml
resource:
  aws_apigatewayv2_route_response:
    example:
      api_id: ${aws_apigatewayv2_api.example.id}
      route_id: ${aws_apigatewayv2_route.example.id}
      route_response_key: $default
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `api_id` - (Required) API identifier.
* `route_id` - (Required) Identifier of the `aws_apigatewayv2_route`.
* `route_response_key` - (Required) Route response key.
* `model_selection_expression` - (Optional) The [model selection expression](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-websocket-api-selection-expressions.html#apigateway-websocket-api-model-selection-expressions) for the route response.
* `response_models` - (Optional) Response models for the route response.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Route response identifier.

## Import

```bash
ytofu import aws_apigatewayv2_route_response.example aabbccddee/1122334/998877
```
