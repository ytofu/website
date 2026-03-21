# Resource: aws_route53_vpc_association_authorization

Authorizes a VPC in a different account to be associated with a local Route53 Hosted Zone.

## Basic Example

```yaml
resource:
  aws_vpc:
    example:
      cidr_block: 10.6.0.0/16
      enable_dns_hostnames: true
      enable_dns_support: true

  aws_route53_zone:
    example:
      name: example.com
      vpc:
        vpc_id: ${aws_vpc.example.id}
      lifecycle:
        ignore_changes: 
          - vpc

  aws_vpc:
    alternate:
      cidr_block: 10.7.0.0/16
      enable_dns_hostnames: true
      enable_dns_support: true

  aws_route53_vpc_association_authorization:
    example:
      vpc_id: ${aws_vpc.alternate.id}
      zone_id: ${aws_route53_zone.example.id}

  aws_route53_zone_association:
    example:
      vpc_id: ${aws_route53_vpc_association_authorization.example.vpc_id}
      zone_id: ${aws_route53_vpc_association_authorization.example.zone_id}```

## Argument Reference

This resource supports the following arguments:

* `zone_id` - (Required) The ID of the private hosted zone that you want to authorize associating a VPC with.
* `vpc_id` - (Required) The VPC to authorize for association with the private hosted zone.
* `vpc_region` - (Optional) The VPC's region. Defaults to the region of the AWS provider.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The calculated unique identifier for the association.

## Timeouts

Configuration options:

* `create` - (Default `20m`)
* `read` - (Default `5m`)
* `delete` - (Default `20m`)

## Import

```bash
ytofu import aws_route53_vpc_association_authorization.example Z123456ABCDEFG:vpc-12345678
```
