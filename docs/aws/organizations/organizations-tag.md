# Organizations Tag

Manage Organizations Tag resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_organizations_organization:
    example:

resource:
  aws_organizations_organizational_unit:
    example:
      name: ExampleOU
      parent_id: ${data.aws_organizations_organization.example.roots[0].id}
      lifecycle:
        ignore_changes: 
          - tags

resource:
  aws_organizations_tag:
    example:
      resource_id: ${aws_organizations_organizational_unit.example.id}
      key: ExampleKey
      value: ExampleValue
```
