# Shield Protection Group

Group Shield protected resources using ytofu YAML.

## All Resources

```yaml
resource:
  aws_shield_protection_group:
    all:
      protection_group_id: all-resources
      aggregation: MAX
      pattern: ALL
```

## By Resource Type

```yaml
resource:
  aws_shield_protection_group:
    albs:
      protection_group_id: alb-group
      aggregation: SUM
      pattern: BY_RESOURCE_TYPE
      resource_type: APPLICATION_LOAD_BALANCER
```

## Arbitrary Members

```yaml
resource:
  aws_shield_protection_group:
    custom:
      protection_group_id: custom-group
      aggregation: MEAN
      pattern: ARBITRARY
      members:
        - ${aws_shield_protection.alb.resource_arn}
        - ${aws_shield_protection.eip.resource_arn}
```
