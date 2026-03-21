# Workmail Domain

Manage Workmail Domain resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_workmail_domain:
    example:
      organization_id: ${aws_workmail_organization.example.id}
      domain_name: example.com
```
