# SSM Default Patch Baseline

Manage SSM Default Patch Baseline resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ssm_default_patch_baseline:
    example:
      baseline_id: ${aws_ssm_patch_baseline.example.id}
      operating_system: ${aws_ssm_patch_baseline.example.operating_system}

resource:
  aws_ssm_patch_baseline:
    example:
      name: example
      approved_patches: 
        - KB123456
```
