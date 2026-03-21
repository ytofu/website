# Resource: aws_synthetics_group_association

Provides a Synthetics Group Association resource.

## Basic Example

```yaml
resource:
  aws_synthetics_group_association:
    example:
      group_name: ${aws_synthetics_group.example.name}
      canary_arn: ${aws_synthetics_canary.example.arn}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `group_name` - (Required) Name of the group that the canary will be associated with.
* `canary_arn` - (Required) ARN of the canary.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `group_name` - Name of the Group.
* `group_id` - ID of the Group.

## Import

```bash
ytofu import aws_synthetics_group_association.example arn:aws:synthetics:us-west-2:123456789012:canary:tf-acc-test-abcd1234,examplename
```
