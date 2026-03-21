# Resource: aws_route53_zone_association

Manages a Route53 Hosted Zone VPC association. VPC associations can only be made on private zones. See the [`aws_route53_vpc_association_authorization` resource](route53_vpc_association_authorization.html) for setting up cross-account associations.

## Basic Example

```yaml
resource:
  aws_vpc:
    primary:
      cidr_block: 10.6.0.0/16
      enable_dns_hostnames: true
      enable_dns_support: true

  aws_vpc:
    secondary:
      cidr_block: 10.7.0.0/16
      enable_dns_hostnames: true
      enable_dns_support: true

  aws_route53_zone:
    example:
      name: example.com
      vpc:
        vpc_id: ${aws_vpc.primary.id}
      lifecycle:
        ignore_changes: 
          - vpc

  aws_route53_zone_association:
    secondary:
      zone_id: ${aws_route53_zone.example.zone_id}
      vpc_id: ${aws_vpc.secondary.id}```

## Argument Reference

This resource supports the following arguments:

* `zone_id` - (Required) The private hosted zone to associate.
* `vpc_id` - (Required) The VPC to associate with the private hosted zone.
* `vpc_region` - (Optional) The VPC's region. Defaults to the region of the AWS provider.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The calculated unique identifier for the association.
* `owning_account` - The account ID of the account that created the hosted zone.

## Timeouts

Configuration options:

* `create` - (Default `30m`)
* `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_route53_zone_association.example Z123456ABCDEFG:vpc-12345678
```
