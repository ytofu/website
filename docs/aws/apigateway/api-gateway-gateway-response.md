# Resource: aws_api_gateway_gateway_response

Provides an API Gateway Gateway Response for a REST API Gateway.

## Basic Example

```yaml
resource:
  aws_api_gateway_rest_api:
    main:
      name: MyDemoAPI

  aws_api_gateway_gateway_response:
    test:
      rest_api_id: ${aws_api_gateway_rest_api.main.id}
      status_code: 401
      response_type: UNAUTHORIZED
      response_templates: 
      response_parameters: ```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be managed. See the [AWS Documentation](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints) for supported values. Defaults to the Region set in the provider configuration.
* `rest_api_id` - (Required) String identifier of the associated REST API.
* `response_type` - (Required) Response type of the associated GatewayResponse. See the [AWS Documentation](https://docs.aws.amazon.com/apigateway/latest/developerguide/supported-gateway-response-types.html) for supported values.
* `status_code` - (Optional) HTTP status code of the Gateway Response.
* `response_templates` - (Optional) Map of templates used to transform the response body.
* `response_parameters` - (Optional) Map of parameters (paths, query strings and headers) of the Gateway Response.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_api_gateway_gateway_response.example 12345abcde/UNAUTHORIZED
```
