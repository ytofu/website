# Organizations Organizational Unit

Manage Organizations Organizational Unit resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_organizations_organizational_unit:
    example:
      name: example
      parent_id: ${aws_organizations_organization.example.roots[0].id}
```
