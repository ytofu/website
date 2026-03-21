# Shield Protection Health Check Association

Manage Shield Protection Health Check Association resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_region:
    current:

data:
  aws_caller_identity:
    current:

data:
  aws_partition:
    current:

resource:
  aws_eip:
    example:
      domain: vpc
      tags:
        Name: example

resource:
  aws_shield_protection:
    example:
      name: example-protection
      resource_arn: "arn:${data.aws_partition.current.partition}:ec2:${data.aws_region.current.region}:${data.aws_caller_identity.current.account_id}:eip-allocation/${aws_eip.example.id}"

resource:
  aws_route53_health_check:
    example:
      ip_address: ${aws_eip.example.public_ip}
      port: 80
      type: HTTP
      resource_path: /ready
      failure_threshold: 3
      request_interval: 30
      tags:
        Name: tf-example-health-check

resource:
  aws_shield_protection_health_check_association:
    example:
      health_check_arn: ${aws_route53_health_check.example.arn}
      shield_protection_id: ${aws_shield_protection.example.id}
```
