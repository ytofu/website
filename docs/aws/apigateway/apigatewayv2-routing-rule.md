# Apigatewayv2 Routing Rule

Manage Apigatewayv2 Routing Rule resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_apigatewayv2_routing_rule:
    example:
      domain_name: test.example.com
      condition:
        match_headers:
          any_of:
            header: X-Example-Header
            value_glob: "example-value-*"
        match_base_paths:
          any_of: 
            - example-path
            - another-path
      action:
        invoke_api:
          api_id: example-api-id
          stage: example-stage
          strip_base_path: true
      priority: 1
```
