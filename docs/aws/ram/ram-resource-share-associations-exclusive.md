# RAM Resource Share Associations Exclusive

Manage RAM Resource Share Associations Exclusive resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ram_resource_share:
    example:
      name: example
      allow_external_principals: true

resource:
  aws_vpc:
    example:
      cidr_block: 10.0.0.0/16

resource:
  aws_subnet:
    example:
      vpc_id: ${aws_vpc.example.id}
      cidr_block: 10.0.1.0/24

resource:
  aws_ram_resource_share_associations_exclusive:
    example:
      resource_share_arn: ${aws_ram_resource_share.example.arn}
      principals:
        - 111111111111
        - 222222222222
      resource_arns:
        - ${aws_subnet.example.arn}
```

## With Organization Principal

```yaml
resource:
  aws_ram_resource_share:
    example:
      name: example

resource:
  aws_vpc:
    example:
      cidr_block: 10.0.0.0/16

resource:
  aws_subnet:
    example:
      vpc_id: ${aws_vpc.example.id}
      cidr_block: 10.0.1.0/24

resource:
  aws_ram_resource_share_associations_exclusive:
    example:
      resource_share_arn: ${aws_ram_resource_share.example.arn}
      principals:
        - ${aws_organizations_organization.example.arn}
      resource_arns: ${aws_subnet.example[*].arn}
```

## With Service Principals

```yaml
resource:
  aws_ram_resource_share:
    example:
      name: example-service-share
      allow_external_principals: true

resource:
  aws_acmpca_certificate_authority:
    example:
      type: ROOT
      certificate_authority_configuration:
        key_algorithm: RSA_4096
        signing_algorithm: SHA512WITHRSA
        subject:
          common_name: example.com

resource:
  aws_ram_resource_share_associations_exclusive:
    example:
      resource_share_arn: ${aws_ram_resource_share.example.arn}
      principals:
        - pca-connector-ad.amazonaws.com
      resource_arns:
        - ${aws_acmpca_certificate_authority.example.arn}
      sources:
        - 111111111111
        - 222222222222
```

## Disallow All Associations

```yaml
resource:
  aws_ram_resource_share_associations_exclusive:
    example:
      resource_share_arn: ${aws_ram_resource_share.example.arn}
```
