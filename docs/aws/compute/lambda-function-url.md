# Lambda Function Url

Manage Lambda Function Url resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lambda_function_url:
    example:
      function_name: ${aws_lambda_function.example.function_name}
      authorization_type: NONE
```

## Function URL with IAM Authentication and CORS Configuration

```yaml
resource:
  aws_lambda_function_url:
    example:
      function_name: ${aws_lambda_function.example.function_name}
      qualifier: my_alias
      authorization_type: AWS_IAM
      invoke_mode: RESPONSE_STREAM
      cors:
        allow_credentials: true
        allow_origins: 
          - "https://example.com"
        allow_methods: 
          - GET
          - POST
        allow_headers: 
          - date
          - keep-alive
        expose_headers: 
          - keep-alive
          - date
        max_age: 86400
```
