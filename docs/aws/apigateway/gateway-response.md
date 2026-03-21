# API Gateway Response

Customize error responses using ytofu YAML.

## Unauthorized Response

```yaml
resource:
  aws_api_gateway_gateway_response:
    unauthorized:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      response_type: UNAUTHORIZED
      status_code: "401"
      response_templates:
        application/json: '{"message": "Unauthorized"}'
      response_parameters:
        gatewayresponse.header.Access-Control-Allow-Origin: "'*'"
```

## Missing Auth Token

```yaml
resource:
  aws_api_gateway_gateway_response:
    missing_auth:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      response_type: MISSING_AUTHENTICATION_TOKEN
      status_code: "403"
      response_templates:
        application/json: '{"message": "Forbidden"}'
```
