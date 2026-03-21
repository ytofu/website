# Resource: aws_route53recoveryreadiness_recovery_group

Provides an AWS Route 53 Recovery Readiness Recovery Group.

## Basic Example

```yaml
resource:
  aws_route53recoveryreadiness_recovery_group:
    example:
      recovery_group_name: my-high-availability-app
```

## Argument Reference

The following arguments are required:

* `recovery_group_name` - (Required) A unique name describing the recovery group.

The following arguments are optional:

* `cells` - (Optional) List of cell arns to add as nested fault domains within this recovery group
* `tags` - (Optional) Key-value mapping of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the recovery group
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

- `delete` - (Default `5m`)

## Import

```bash
ytofu import aws_route53recoveryreadiness_recovery_group.my-high-availability-app my-high-availability-app
```
