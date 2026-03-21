# Route53profiles Resource Association

Manage Route53profiles Resource Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_route53profiles_profile:
    example:
      name: example

resource:
  aws_vpc:
    example:
      cidr: 10.0.0.0/16

resource:
  aws_route53_zone:
    example:
      name: example.com
      vpc:
        vpc_id: ${aws_vpc.example.id}

resource:
  aws_route53profiles_resource_association:
    example:
      name: example
      profile_id: ${aws_route53profiles_profile.example.id}
      resource_arn: ${aws_route53_zone.example.arn}
```
