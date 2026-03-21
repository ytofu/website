# API Gateway API Key

Create API keys using ytofu YAML.

## Basic API Key

```yaml
resource:
  aws_api_gateway_api_key:
    example:
      name: example
```

## With Value

```yaml
resource:
  aws_api_gateway_api_key:
    example:
      name: example
      value: example-api_key_value
```
