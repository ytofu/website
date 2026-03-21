# Bedrockagentcore Workload Identity

Manage Bedrockagentcore Workload Identity resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_bedrockagentcore_workload_identity:
    example:
      name: example-workload-identity
      allowed_resource_oauth2_return_urls:
        - "https://example.com/callback"
```

## Workload Identity with Multiple Return URLs

```yaml
resource:
  aws_bedrockagentcore_workload_identity:
    example:
      name: example-workload-identity
      allowed_resource_oauth2_return_urls:
        - "https://app.example.com/oauth/callback"
        - "https://api.example.com/auth/return"
        - "https://example.com/callback"
```
