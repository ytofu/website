# Route53 VPC Association Authorization

Manage Route53 VPC Association Authorization resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc:
    example:
      cidr_block: 10.6.0.0/16
      enable_dns_hostnames: true
      enable_dns_support: true

resource:
  aws_route53_zone:
    example:
      name: example.com
      vpc:
        vpc_id: ${aws_vpc.example.id}
      lifecycle:
        ignore_changes: 
          - vpc

resource:
  aws_vpc:
    alternate:
      cidr_block: 10.7.0.0/16
      enable_dns_hostnames: true
      enable_dns_support: true

resource:
  aws_route53_vpc_association_authorization:
    example:
      vpc_id: ${aws_vpc.alternate.id}
      zone_id: ${aws_route53_zone.example.id}

resource:
  aws_route53_zone_association:
    example:
      vpc_id: ${aws_route53_vpc_association_authorization.example.vpc_id}
      zone_id: ${aws_route53_vpc_association_authorization.example.zone_id}
```
