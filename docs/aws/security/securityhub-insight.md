# Securityhub Insight

Manage Securityhub Insight resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_securityhub_account:
    example:

resource:
  aws_securityhub_insight:
    example:
      filters:
        aws_account_id:
          comparison: EQUALS
          value: 1234567890
        aws_account_id:
          comparison: EQUALS
          value: 09876543210
      group_by_attribute: AwsAccountId
      name: example-insight
      depends_on: 
        - ${aws_securityhub_account.example}
```

## Filter by date range

```yaml
resource:
  aws_securityhub_account:
    example:

resource:
  aws_securityhub_insight:
    example:
      filters:
        created_at:
          date_range:
            unit: DAYS
            value: 5
      group_by_attribute: CreatedAt
      name: example-insight
      depends_on: 
        - ${aws_securityhub_account.example}
```

## Filter by destination IPv4 address

```yaml
resource:
  aws_securityhub_account:
    example:

resource:
  aws_securityhub_insight:
    example:
      filters:
        network_destination_ipv4:
          cidr: 10.0.0.0/16
      group_by_attribute: NetworkDestinationIpV4
      name: example-insight
      depends_on: 
        - ${aws_securityhub_account.example}
```

## Filter by finding's confidence

```yaml
resource:
  aws_securityhub_account:
    example:

resource:
  aws_securityhub_insight:
    example:
      filters:
        confidence:
          gte: 80
      group_by_attribute: Confidence
      name: example-insight
      depends_on: 
        - ${aws_securityhub_account.example}
```

## Filter by resource tags

```yaml
resource:
  aws_securityhub_account:
    example:

resource:
  aws_securityhub_insight:
    example:
      filters:
        resource_tags:
          comparison: EQUALS
          key: Environment
          value: Production
      group_by_attribute: ResourceTags
      name: example-insight
      depends_on: 
        - ${aws_securityhub_account.example}
```
