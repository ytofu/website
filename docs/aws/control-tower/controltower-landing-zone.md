# Resource: aws_controltower_landing_zone

Creates a new landing zone using Control Tower. For more information on usage, please see the
[AWS Control Tower Landing Zone User Guide](https://docs.aws.amazon.com/controltower/latest/userguide/how-control-tower-works.html).

## Basic Example

```yaml
resource:
  aws_controltower_landing_zone:
    example:
      manifest_json: file-content
      version: 3.2
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `manifest_json` - (Required) The manifest JSON file is a text file that describes your AWS resources. For examples, review [Launch your landing zone](https://docs.aws.amazon.com/controltower/latest/userguide/lz-api-launch).
* `version` - (Required) The landing zone version.
* `tags` - (Optional) Tags to apply to the landing zone. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The identifier of the landing zone.
* `arn` - The ARN of the landing zone.
* `drift_status` - The drift status summary of the landing zone.
    * `status` - The drift status of the landing zone.
* `latest_available_version` - The latest available version of the landing zone.
* `tags_all` - A map of tags assigned to the landing zone, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

- `create` - (Default `120m`)
- `update` - (Default `120m`)
- `delete` - (Default `120m`)

## Import

```bash
ytofu import aws_controltower_landing_zone.example 1A2B3C4D5E6F7G8H
```
