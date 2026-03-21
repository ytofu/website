# Workmail Default Domain

Manage Workmail Default Domain resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_workmail_organization:
    example:
      organization_alias: example-org

resource:
  aws_workmail_default_domain:
    example:
      organization_id: ${aws_workmail_organization.example.id}
      domain_name: ${aws_workmail_organization.example.default_mail_domain}
```
