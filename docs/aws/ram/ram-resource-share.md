# RAM Resource Share

Manage RAM Resource Share resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ram_resource_share:
    example:
      name: example
      allow_external_principals: true
      tags:
        Environment: Production
```
