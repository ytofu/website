# API Gateway Model

Manage API Gateway Model resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_api_gateway_rest_api:
    MyDemoAPI:
      name: MyDemoAPI
      description: This is my API for demonstration purposes

resource:
  aws_api_gateway_model:
    MyDemoModel:
      rest_api_id: ${aws_api_gateway_rest_api.MyDemoAPI.id}
      name: user
      description: a JSON schema
      content_type: application/json
      schema: '{ "type": "object" }'
```
