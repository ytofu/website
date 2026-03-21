# Customerprofiles Profile

Manage Customerprofiles Profile resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_customerprofiles_domain:
    example:
      domain_name: example

resource:
  aws_customerprofiles_profile:
    example:
      domain_name: ${aws_customerprofiles_domain.example.domain_name}
```
