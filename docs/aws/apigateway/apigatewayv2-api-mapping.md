# Resource: aws_apigatewayv2_api_mapping

Manages an Amazon API Gateway Version 2 API mapping.
More information can be found in the [Amazon API Gateway Developer Guide](https://docs.aws.amazon.com/apigateway/latest/developerguide/how-to-custom-domains.html).

## Basic Example

```yaml
resource:
  aws_apigatewayv2_api_mapping:
    example:
      api_id: ${aws_apigatewayv2_api.example.id}
      domain_name: ${aws_apigatewayv2_domain_name.example.id}
      stage: ${aws_apigatewayv2_stage.example.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `api_id` - (Required) API identifier.
* `domain_name` - (Required) Domain name. Use the `aws_apigatewayv2_domain_name` resource to configure a domain name.
* `stage` - (Required) API stage. Use the `aws_apigatewayv2_stage` resource to configure an API stage.
* `api_mapping_key` - (Optional) The API mapping key. Refer to [REST API](https://docs.aws.amazon.com/apigateway/latest/developerguide/rest-api-mappings.html), [HTTP API](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-mappings.html) or [WebSocket API](https://docs.aws.amazon.com/apigateway/latest/developerguide/websocket-api-mappings.html).

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - API mapping identifier.

## Import

```bash
ytofu import aws_apigatewayv2_api_mapping.example 1122334/ws-api.example.com
```
