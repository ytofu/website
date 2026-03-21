# Resource: aws_route53recoveryreadiness_cell

Provides an AWS Route 53 Recovery Readiness Cell.

## Basic Example

```yaml
resource:
  aws_route53recoveryreadiness_cell:
    example:
      cell_name: us-west-2-failover-cell
```

## Argument Reference

The following arguments are required:

* `cell_name` - (Required) Unique name describing the cell.

The following arguments are optional:

* `cells` - (Optional) List of cell arns to add as nested fault domains within this cell.
* `tags` - (Optional) Key-value mapping of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the cell
* `parent_readiness_scopes` - List of readiness scopes (recovery groups or cells) that contain this cell.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

- `delete` - (Default `5m`)

## Import

```bash
ytofu import aws_route53recoveryreadiness_cell.us-west-2-failover-cell us-west-2-failover-cell
```
