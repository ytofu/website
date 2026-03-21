# Resource: aws_route53recoverycontrolconfig_control_panel

Provides an AWS Route 53 Recovery Control Config Control Panel.

## Basic Example

```yaml
resource:
  aws_route53recoverycontrolconfig_control_panel:
    example:
      name: balmorhea
      cluster_arn: "arn:aws:route53-recovery-control::123456789012:cluster/8d47920e-d789-437d-803a-2dcc4b204393"
```

## Argument Reference

The following arguments are required:

* `cluster_arn` - (Required) ARN of the cluster in which this control panel will reside.
* `name` - (Required) Name describing the control panel.

The following arguments are optional:

* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the control panel.
* `default_control_panel` - Whether a control panel is default.
* `routing_control_count` - Number routing controls in a control panel.
* `status` - Status of control panel: `PENDING` when it is being created/updated, `PENDING_DELETION` when it is being deleted, and `DEPLOYED` otherwise.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_route53recoverycontrolconfig_control_panel.mypanel arn:aws:route53-recovery-control::313517334327:controlpanel/1bfba17df8684f5dab0467b71424f7e8
```
