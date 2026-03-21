# API Gateway Resource

Create API resources (paths) using ytofu YAML.

## Basic Resource

```yaml
resource:
  aws_api_gateway_resource:
    example:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      parent_id: ${aws_api_gateway_rest_api.example.root_resource_id}
      path_part: mydemoresource
```

## Nested Resource

```yaml
resource:
  aws_api_gateway_resource:
    v1:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      parent_id: ${aws_api_gateway_rest_api.example.root_resource_id}
      path_part: v1

  aws_api_gateway_resource:
    users:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      parent_id: ${aws_api_gateway_resource.v1.id}
      path_part: users

  aws_api_gateway_resource:
    user:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      parent_id: ${aws_api_gateway_resource.users.id}
      path_part: "{userId}"
```
