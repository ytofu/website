# Ce Cost Allocation Tag

Manage Ce Cost Allocation Tag resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ce_cost_allocation_tag:
    example:
      tag_key: example
      status: Active
```

## Account Tags as Cost Allocation Tags

```yaml
resource:
  aws_ce_cost_allocation_tag:
    example:
      tag_key: accountTag/example
      status: Active
```
