# Route53profiles Association

Manage Route53profiles Association resources using ytofu YAML.

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
  aws_route53profiles_association:
    example:
      name: example
      profile_id: ${aws_route53profiles_profile.example.id}
      resource_id: ${aws_vpc.example.id}
      tags:
        Environment: dev
```
