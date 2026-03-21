# Shield Protection Group

Manage Shield Protection Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_shield_protection_group:
    example:
      protection_group_id: example
      aggregation: MAX
      pattern: ALL
```

## Create protection group for arbitrary number of resources

```yaml
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

resource:
  aws_shield_protection_group:
    example:
      depends_on: 
        - ${aws_shield_protection.example}
      protection_group_id: example
      aggregation: MEAN
      pattern: ARBITRARY
      members: 
        - "arn:aws:ec2:${data.aws_region.current.region}:${data.aws_caller_identity.current.account_id}:eip-allocation/${aws_eip.example.id}"
```

## Create protection group for a type of resource

```yaml
resource:
  aws_shield_protection_group:
    example:
      protection_group_id: example
      aggregation: SUM
      pattern: BY_RESOURCE_TYPE
      resource_type: ELASTIC_IP_ALLOCATION
```
