# Securityhub Finding Aggregator

Manage Securityhub Finding Aggregator resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_securityhub_account:
    example:

resource:
  aws_securityhub_finding_aggregator:
    example:
      linking_mode: ALL_REGIONS
      depends_on: 
        - ${aws_securityhub_account.example}
```

## All Regions Except Specified Regions Usage

```yaml
resource:
  aws_securityhub_account:
    example:

resource:
  aws_securityhub_finding_aggregator:
    example:
      linking_mode: ALL_REGIONS_EXCEPT_SPECIFIED
      specified_regions: 
        - eu-west-1
        - eu-west-2
      depends_on: 
        - ${aws_securityhub_account.example}
```

## Specified Regions Usage

```yaml
resource:
  aws_securityhub_account:
    example:

resource:
  aws_securityhub_finding_aggregator:
    example:
      linking_mode: SPECIFIED_REGIONS
      specified_regions: 
        - eu-west-1
        - eu-west-2
      depends_on: 
        - ${aws_securityhub_account.example}
```

## No Regions Usage

```yaml
resource:
  aws_securityhub_account:
    example:

resource:
  aws_securityhub_finding_aggregator:
    example:
      linking_mode: NO_REGIONS
      depends_on: 
        - ${aws_securityhub_account.example}
```
