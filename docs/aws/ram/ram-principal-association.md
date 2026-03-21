# RAM Principal Association

Manage RAM Principal Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ram_resource_share:
    example:
      allow_external_principals: true

resource:
  aws_ram_principal_association:
    example:
      principal: 111111111111
      resource_share_arn: ${aws_ram_resource_share.example.arn}
```

## AWS Organization

```yaml
resource:
  aws_ram_principal_association:
    example:
      principal: ${aws_organizations_organization.example.arn}
      resource_share_arn: ${aws_ram_resource_share.example.arn}
```
