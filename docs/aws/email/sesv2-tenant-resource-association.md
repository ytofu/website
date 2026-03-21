# Sesv2 Tenant Resource Association

Manage Sesv2 Tenant Resource Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sesv2_tenant_resource_association:
    example:
      tenant_name: example-tenant
      resource_arn: "arn:aws:ses:us-east-1:123456789012:configuration-set/example"
```
