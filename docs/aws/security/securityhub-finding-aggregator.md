# Resource: aws_securityhub_finding_aggregator

Manages a Security Hub finding aggregator. Security Hub needs to be enabled in a region in order for the aggregator to pull through findings.

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

## Argument Reference

This resource supports the following arguments:

- `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
- `linking_mode` - (Required) Indicates whether to aggregate findings from all of the available Regions or from a specified list. The options are `ALL_REGIONS`, `ALL_REGIONS_EXCEPT_SPECIFIED`, `SPECIFIED_REGIONS` or `NO_REGIONS`. When `ALL_REGIONS` or `ALL_REGIONS_EXCEPT_SPECIFIED` are used, Security Hub will automatically aggregate findings from new Regions as Security Hub supports them and you opt into them.
- `specified_regions` - (Optional) List of regions to include or exclude (required if `linking_mode` is set to `ALL_REGIONS_EXCEPT_SPECIFIED` or `SPECIFIED_REGIONS`)

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

- `arn` - Amazon Resource Name (ARN) of the Security Hub finding aggregator.

## Import

```bash
ytofu import aws_securityhub_finding_aggregator.example arn:aws:securityhub:eu-west-1:123456789098:finding-aggregator/abcd1234-abcd-1234-1234-abcdef123456
```
