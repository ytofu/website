# Shield Protection

Manage Shield Protection resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_availability_zones:
    available:

data:
  aws_region:
    current:

data:
  aws_caller_identity:
    current:

resource:
  aws_eip:
    example:
      domain: vpc

resource:
  aws_shield_protection:
    example:
      name: example
      resource_arn: "arn:aws:ec2:${data.aws_region.current.region}:${data.aws_caller_identity.current.account_id}:eip-allocation/${aws_eip.example.id}"
      tags:
        Environment: Dev
```
