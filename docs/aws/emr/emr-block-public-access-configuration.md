# EMR Block Public Access Configuration

Manage EMR Block Public Access Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_emr_block_public_access_configuration:
    example:
      block_public_security_group_rules: true
```

## Default Configuration

```yaml
resource:
  aws_emr_block_public_access_configuration:
    example:
      block_public_security_group_rules: true
      permitted_public_security_group_rule_range:
        min_range: 22
        max_range: 22
```

## Multiple Permitted Public Security Group Rule Ranges

```yaml
resource:
  aws_emr_block_public_access_configuration:
    example:
      block_public_security_group_rules: true
      permitted_public_security_group_rule_range:
        min_range: 22
        max_range: 22
      permitted_public_security_group_rule_range:
        min_range: 100
        max_range: 101
```

## Disabling Block Public Access

```yaml
resource:
  aws_emr_block_public_access_configuration:
    example:
      block_public_security_group_rules: false
```
