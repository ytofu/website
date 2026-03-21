# Bedrockagentcore API Key Credential Provider

Manage Bedrockagentcore API Key Credential Provider resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_bedrockagentcore_api_key_credential_provider:
    example:
      name: example-api-key-provider
      api_key: your-api-key-here
```

## Write-Only API Key (Recommended for Production)

```yaml
resource:
  aws_bedrockagentcore_api_key_credential_provider:
    example:
      name: example-api-key-provider
      api_key_wo: your-api-key-here
      api_key_wo_version: 1
```
