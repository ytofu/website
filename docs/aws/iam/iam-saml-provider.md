# IAM SAML Provider

Manage IAM SAML Provider resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iam_saml_provider:
    default:
      name: myprovider
      saml_metadata_document: file-content
```
