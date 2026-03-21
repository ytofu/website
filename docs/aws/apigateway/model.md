# API Gateway Model

Define request/response models using ytofu YAML.

## JSON Model

```yaml
resource:
  aws_api_gateway_model:
    example:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      name: user
      description: User model
      content_type: application/json
      schema: |
        {
          "$schema": "http://json-schema.org/draft-04/schema#",
          "title": "User",
          "type": "object",
          "properties": {
            "id": {"type": "integer"},
            "name": {"type": "string"},
            "email": {"type": "string"}
          }
        }
```
