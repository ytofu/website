# Resource: aws_location_tracker

Provides a Location Service Tracker.

## Basic Example

```yaml
resource:
  aws_location_tracker:
    example:
      tracker_name: example
```

## Argument Reference

The following arguments are required:

* `tracker_name` - (Required) The name of the tracker resource.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional) The optional description for the tracker resource.
* `kms_key_id` - (Optional) A key identifier for an AWS KMS customer managed key assigned to the Amazon Location resource.
* `position_filtering` - (Optional) The position filtering method of the tracker resource. Valid values: `TimeBased`, `DistanceBased`, `AccuracyBased`. Default: `TimeBased`.
* `tags` - (Optional) Key-value tags for the tracker. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `create_time` - The timestamp for when the tracker resource was created in ISO 8601 format.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.
* `tracker_arn` - The Amazon Resource Name (ARN) for the tracker resource. Used when you need to specify a resource across all AWS.
* `update_time` - The timestamp for when the tracker resource was last updated in ISO 8601 format.

## Import

```bash
ytofu import aws_location_tracker.example example
```
