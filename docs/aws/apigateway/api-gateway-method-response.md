# Resource: aws_api_gateway_method_response

Provides an HTTP Method Response for an API Gateway Resource. More information about API Gateway method responses can be found in the [Amazon API Gateway Developer Guide](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-method-settings-method-response.html).

## Basic Example

```yaml
resource:
  aws_api_gateway_rest_api:
    MyDemoAPI:
      name: MyDemoAPI
      description: This is my API for demonstration purposes

resource:
  aws_api_gateway_resource:
    MyDemoResource:
      rest_api_id: ${aws_api_gateway_rest_api.MyDemoAPI.id}
      parent_id: ${aws_api_gateway_rest_api.MyDemoAPI.root_resource_id}
      path_part: mydemoresource

resource:
  aws_api_gateway_method:
    MyDemoMethod:
      rest_api_id: ${aws_api_gateway_rest_api.MyDemoAPI.id}
      resource_id: ${aws_api_gateway_resource.MyDemoResource.id}
      http_method: GET
      authorization: NONE

resource:
  aws_api_gateway_integration:
    MyDemoIntegration:
      rest_api_id: ${aws_api_gateway_rest_api.MyDemoAPI.id}
      resource_id: ${aws_api_gateway_resource.MyDemoResource.id}
      http_method: ${aws_api_gateway_method.MyDemoMethod.http_method}
      type: MOCK

resource:
  aws_api_gateway_method_response:
    response_200:
      rest_api_id: ${aws_api_gateway_rest_api.MyDemoAPI.id}
      resource_id: ${aws_api_gateway_resource.MyDemoResource.id}
      http_method: ${aws_api_gateway_method.MyDemoMethod.http_method}
      status_code: 200
```

## Response with Custom Header and Model

```yaml
resource:
  aws_api_gateway_rest_api:
    MyDemoAPI:
      name: MyDemoAPI
      description: This is my API for demonstration purposes

resource:
  aws_api_gateway_resource:
    MyDemoResource:
      rest_api_id: ${aws_api_gateway_rest_api.MyDemoAPI.id}
      parent_id: ${aws_api_gateway_rest_api.MyDemoAPI.root_resource_id}
      path_part: mydemoresource

resource:
  aws_api_gateway_method:
    MyDemoMethod:
      rest_api_id: ${aws_api_gateway_rest_api.MyDemoAPI.id}
      resource_id: ${aws_api_gateway_resource.MyDemoResource.id}
      http_method: GET
      authorization: NONE

resource:
  aws_api_gateway_integration:
    MyDemoIntegration:
      rest_api_id: ${aws_api_gateway_rest_api.MyDemoAPI.id}
      resource_id: ${aws_api_gateway_resource.MyDemoResource.id}
      http_method: ${aws_api_gateway_method.MyDemoMethod.http_method}
      type: MOCK

resource:
  aws_api_gateway_model:
    MyDemoResponseModel:
      rest_api_id: ${aws_api_gateway_rest_api.MyDemoAPI.id}
      name: MyDemoResponseModel
      description: API response for MyDemoMethod
      content_type: application/json
      schema: '{ "$schema" = "http://json-schema.org/draft-04/schema#" "title": "MyDemoResponse" "type": "object" "properties": { "Message": { "type": "string" } } }'

resource:
  aws_api_gateway_method_response:
    response_200:
      rest_api_id: ${aws_api_gateway_rest_api.MyDemoAPI.id}
      resource_id: ${aws_api_gateway_resource.MyDemoResource.id}
      http_method: ${aws_api_gateway_method.MyDemoMethod.http_method}
      status_code: 200
      response_models: 
      response_parameters: 
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `rest_api_id` - (Required) The string identifier of the associated REST API.
* `resource_id` - (Required) The Resource identifier for the method resource.
* `http_method` - (Required) The HTTP verb of the method resource (`GET`, `POST`, `PUT`, `DELETE`, `HEAD`, `OPTIONS`, `ANY`).
* `status_code` - (Required) The method response's status code.
* `response_models` - (Optional) A map specifying the model resources used for the response's content type. Response models are represented as a key/value map, with a content type as the key and a Model name as the value.
* `response_parameters` - (Optional) A map specifying required or optional response parameters that API Gateway can send back to the caller. A key defines a method response header name and the associated value is a boolean flag indicating whether the method response parameter is required. The method response header names must match the pattern of `method.response.header.{name}`, where `name` is a valid and unique header name.

The response parameter names defined here are available in the integration response to be mapped from an integration response header expressed in `integration.response.header.{name}`, a static value enclosed within a pair of single quotes (e.g., '`application/json'`), or a JSON expression from the back-end response payload in the form of `integration.response.body.{JSON-expression}`, where `JSON-expression` is a valid JSON expression without the `$` prefix.)

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_api_gateway_method_response.example 12345abcde/67890fghij/GET/200
```
