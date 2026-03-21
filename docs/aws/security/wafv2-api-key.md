# Wafv2 API Key

Manage Wafv2 API Key resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_wafv2_api_key:
    example:
      scope: REGIONAL
      token_domains: 
        - example.com
```
