# Resource: aws_detective_organization_configuration

Manages the Detective Organization Configuration in the current AWS Region. The AWS account utilizing this resource must have been assigned as a delegated Organization administrator account, e.g., via the `aws_detective_organization_admin_account` resource. More information about Organizations support in Detective can be found in the [Detective User Guide](https://docs.aws.amazon.com/detective/latest/adminguide/accounts-orgs-transition.html).

## Basic Example

```yaml
resource:
  aws_detective_graph:
    example:
      enable: true

resource:
  aws_detective_organization_configuration:
    example:
      auto_enable: true
      graph_arn: ${aws_detective_graph.example.graph_arn}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `auto_enable` - (Required) When this setting is enabled, all new accounts that are created in, or added to, the organization are added as a member accounts of the organization’s Detective delegated administrator and Detective is enabled in that AWS Region.
* `graph_arn` - (Required) ARN of the behavior graph.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Identifier of the Detective Graph.

## Import

```bash
ytofu import aws_detective_organization_configuration.example arn:aws:detective:us-east-1:123456789012:graph:00b00fd5aecc0ab60a708659477e9617
```
