# Resource: aws_auditmanager_framework

ytofu resource for managing an AWS Audit Manager Framework.

## Basic Example

```yaml
resource:
  aws_auditmanager_framework:
    test:
      name: example
      control_sets:
        name: example
        controls:
          id: ${aws_auditmanager_control.test_1.id}
        controls:
          id: ${aws_auditmanager_control.test_2.id}
```

## Argument Reference

The following arguments are required:

* `name` - (Required) Name of the framework.
* `control_sets` - (Required) Configuration block(s) for the control sets that are associated with the framework. See [`control_sets` Block](#control_sets-block) below for details.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `compliance_type` - (Optional) Compliance type that the new custom framework supports, such as `CIS` or `HIPAA`.
* `description` - (Optional) Description of the framework.
* `tags` - (Optional) A map of tags to assign to the framework. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### `control_sets` Block

The `control_sets` configuration block supports the following arguments:

* `name` - (Required) Name of the control set.
* `controls` - (Required) Configuration block(s) for the controls within the control set. See [`controls` Block](#controls-block) below for details.

### `controls` Block

The `controls` configuration block supports the following arguments:

* `id` - (Required) Unique identifier of the control.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Amazon Resource Name (ARN) of the framework.
* `control_sets[*].id` - Unique identifier for the framework control set.
* `id` - Unique identifier for the framework.
* `framework_type` - Framework type, such as a custom framework or a standard framework.

## Import

```bash
ytofu import aws_auditmanager_framework.example abc123-de45
```
