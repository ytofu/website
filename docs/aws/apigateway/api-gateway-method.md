# Resource: aws_api_gateway_method

Provides a HTTP Method for an API Gateway Resource.

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
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `rest_api_id` - (Required) ID of the associated REST API
* `resource_id` - (Required) API resource ID
* `http_method` - (Required) HTTP Method (`GET`, `POST`, `PUT`, `DELETE`, `HEAD`, `OPTIONS`, `ANY`)
* `authorization` - (Required) Type of authorization used for the method (`NONE`, `CUSTOM`, `AWS_IAM`, `COGNITO_USER_POOLS`)
* `authorizer_id` - (Optional) Authorizer id to be used when the authorization is `CUSTOM` or `COGNITO_USER_POOLS`
* `authorization_scopes` - (Optional) Authorization scopes used when the authorization is `COGNITO_USER_POOLS`
* `api_key_required` - (Optional) Specify if the method requires an API key
* `operation_name` - (Optional) Function name that will be given to the method when generating an SDK through API Gateway. If omitted, API Gateway will generate a function name based on the resource path and HTTP verb.
* `request_models` - (Optional) Map of the API models used for the request's content type
  where key is the content type (e.g., `application/json`)
  and value is either `Error`, `Empty` (built-in models) or `aws_api_gateway_model`'s `name`.
* `request_validator_id` - (Optional) ID of a `aws_api_gateway_request_validator`
* `request_parameters` - (Optional) Map of request parameters (from the path, query string and headers) that should be passed to the integration. The boolean value indicates whether the parameter is required (`true`) or optional (`false`).
  For example: `request_parameters = {"method.request.header.X-Some-Header" = true "method.request.querystring.some-query-param" = true}` would define that the header `X-Some-Header` and the query string `some-query-param` must be provided in the request.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_api_gateway_method.example 12345abcde/67890fghij/GET
```
