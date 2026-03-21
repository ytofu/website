# API Gateway Method Response

Manage API Gateway Method Response resources using ytofu YAML.

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
