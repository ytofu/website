# AWS Config Aggregator

Aggregate Config data from multiple accounts using ytofu YAML.

## Organization Aggregator

```yaml
resource:
  aws_config_configuration_aggregator:
    organization:
      name: example
      organization_aggregation_source:
        all_regions: true
        role_arn: ${aws_iam_role.organization.arn}
```

## Account Aggregator

```yaml
resource:
  aws_config_configuration_aggregator:
    account:
      name: example
      account_aggregation_source:
        account_ids:
          - "123456789012"
        regions:
          - us-east-1
          - us-west-2
```
