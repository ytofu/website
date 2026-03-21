# Resource: aws_ssm_patch_group

Provides an SSM Patch Group resource

## Basic Example

```yaml
resource:
  aws_ssm_patch_baseline:
    production:
      name: patch-baseline
      approved_patches: 
        - KB123456

  aws_ssm_patch_group:
    patchgroup:
      baseline_id: ${aws_ssm_patch_baseline.production.id}
      patch_group: patch-group-name```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `baseline_id` - (Required) The ID of the patch baseline to register the patch group with.
* `patch_group` - (Required) The name of the patch group that should be registered with the patch baseline.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The name of the patch group and ID of the patch baseline separated by a comma (`,`).
