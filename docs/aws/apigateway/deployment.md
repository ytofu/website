# API Gateway Deployment

Deploy API Gateway REST APIs using ytofu YAML.

## Basic Deployment

```yaml
resource:
  aws_api_gateway_deployment:
    example:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      triggers:
        redeployment: ${sha1(jsonencode(aws_api_gateway_rest_api.example.body))}
      lifecycle:
        create_before_destroy: true
```
