# Rbin Rule

Manage Rbin Rule resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_rbin_rule:
    example:
      description: Example tag-level retention rule
      resource_type: EBS_SNAPSHOT
      resource_tags:
        resource_tag_key: tag_key
        resource_tag_value: tag_value
      retention_period:
        retention_period_value: 10
        retention_period_unit: DAYS
      tags: 
```

## Region-Level Retention Rule

```yaml
resource:
  aws_rbin_rule:
    example:
      description: Example region-level retention rule with exclusion tags
      resource_type: EC2_IMAGE
      exclude_resource_tags:
        resource_tag_key: tag_key
        resource_tag_value: tag_value
      retention_period:
        retention_period_value: 10
        retention_period_unit: DAYS
      tags: 
```
