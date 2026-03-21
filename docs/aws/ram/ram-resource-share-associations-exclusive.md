# Resource: aws_ram_resource_share_associations_exclusive

ytofu resource for maintaining exclusive management of principal and resource associations for an AWS RAM (Resource Access Manager) Resource Share.

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

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `resource_share_arn` - (Required) The Amazon Resource Name (ARN) of the resource share. Changing this value forces creation of a new resource.
* `principals` - (Optional) A set of principals to associate with the resource share. Principals not configured in this argument will be removed. Valid values include:
    * AWS account ID (exactly 12 digits, e.g., `123456789012`)
    * AWS Organizations Organization ARN (e.g., `arn:aws:organizations::123456789012:organization/o-exampleorgid`)
    * AWS Organizations Organizational Unit ARN (e.g., `arn:aws:organizations::123456789012:ou/o-exampleorgid/ou-examplerootid-exampleouid`)
    * IAM role ARN (e.g., `arn:aws:iam::123456789012:role/example-role`)
    * IAM user ARN (e.g., `arn:aws:iam::123456789012:user/example-user`)
    * Service principal (e.g., `ec2.amazonaws.com`)
* `resource_arns` - (Optional) A set of Amazon Resource Names (ARNs) of resources to associate with the resource share. Resources not configured in this argument will be removed.
* `sources` - (Optional) A set of AWS account IDs that restrict which accounts a service principal can access resources from. This argument can only be specified when `principals` contains only service principals. When specified, it limits the source accounts from which the service can access the shared resources.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_ram_resource_share_associations_exclusive.example arn:aws:ram:eu-west-1:123456789012:resource-share/73da1ab9-b94a-4ba3-8eb4-45917f7f4b12
```
