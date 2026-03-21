# Ssoadmin Trusted Token Issuer

Manage Ssoadmin Trusted Token Issuer resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_ssoadmin_instances:
    example:

resource:
  aws_ssoadmin_trusted_token_issuer:
    example:
      name: example
      instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}
      trusted_token_issuer_type: OIDC_JWT
      trusted_token_issuer_configuration:
        oidc_jwt_configuration:
          claim_attribute_path: email
          identity_store_attribute_path: emails.value
          issuer_url: "https://example.com"
          jwks_retrieval_option: OPEN_ID_DISCOVERY
```
