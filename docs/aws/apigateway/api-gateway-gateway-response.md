# API Gateway Gateway Response

Manage API Gateway Gateway Response resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_api_gateway_rest_api:
    main:
      name: MyDemoAPI

resource:
  aws_api_gateway_gateway_response:
    test:
      rest_api_id: ${aws_api_gateway_rest_api.main.id}
      status_code: 401
      response_type: UNAUTHORIZED
      response_templates: 
      response_parameters: 
```
