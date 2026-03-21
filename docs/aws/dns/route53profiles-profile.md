# Resource: aws_route53profiles_profile

ytofu resource for managing an AWS Route 53 Profile.

## Basic Example

```yaml
resource:
  aws_route53profiles_profile:
    example:
      name: example
      tags:
        Environment: dev
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) Name of the Profile.
* `tags` - (Optional) Map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Profile.
* `id` - ID of the Profile.
* `name` - Name of the Profile.
* `share_status` - Share status of the Profile.
* `status` - Status of the Profile.
* `status_message` - Status message of the Profile.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

* `create` - (Default `30m`)
* `read` - (Default `30m`)
* `update` - (Default `30m`)
* `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_route53profiles_profile.example rp-12345678
```
