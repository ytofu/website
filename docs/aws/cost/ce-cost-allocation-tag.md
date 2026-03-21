# Resource: aws_ce_cost_allocation_tag

Provides a CE Cost Allocation Tag.

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

## Argument Reference

The following arguments are required:

* `tag_key` - (Required) The key for the cost allocation tag.
* `status` - (Required) The status of a cost allocation tag. Valid values are `Active` and `Inactive`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The key for the cost allocation tag.
* `type` - The type of cost allocation tag.

## Import

```bash
ytofu import aws_ce_cost_allocation_tag.example key
```
