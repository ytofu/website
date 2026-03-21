# Resource: aws_inspector_assessment_target

Provides an Inspector Classic Assessment Target

## Basic Example

```yaml
resource:
  aws_inspector_resource_group:
    bar:
      tags:
        Name: foo
        Env: bar

resource:
  aws_inspector_assessment_target:
    foo:
      name: assessment target
      resource_group_arn: ${aws_inspector_resource_group.bar.arn}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name of the assessment target.
* `resource_group_arn` (Optional) Inspector Resource Group Amazon Resource Name (ARN) stating tags for instance matching. If not specified, all EC2 instances in the current AWS account and region are included in the assessment target.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The target assessment ARN.

## Import

```bash
ytofu import aws_inspector_assessment_target.example arn:aws:inspector:us-east-1:123456789012:target/0-xxxxxxx
```
