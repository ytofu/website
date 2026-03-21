# Resource: aws_pinpointsmsvoicev2_opt_out_list

Manages an AWS End User Messaging SMS opt-out list.

## Basic Example

```yaml
resource:
  aws_pinpointsmsvoicev2_opt_out_list:
    example:
      name: example-opt-out-list
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name of the opt-out list.
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the opt-out list.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_pinpointsmsvoicev2_opt_out_list.example example-opt-out-list
```
