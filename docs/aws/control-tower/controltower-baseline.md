# Controltower Baseline

Manage Controltower Baseline resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_controltower_baseline:
    example:
      baseline_identifier: "arn:aws:controltower:us-east-1::baseline/17BSJV3IGJ2QSGA2"
      baseline_version: 4.0
      target_identifier: ${aws_organizations_organizational_unit.test.arn}
      parameters:
        key: IdentityCenterEnabledBaselineArn
        value: "arn:aws:controltower:us-east-1:664418989480:enabledbaseline/XALULM96QHI525UOC"
```
