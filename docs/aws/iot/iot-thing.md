# Resource: aws_iot_thing

Creates and manages an AWS IoT Thing.

## Basic Example

```yaml
resource:
  aws_iot_thing:
    example:
      name: example
      attributes:
        First: examplevalue
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name of the thing.
* `attributes` - (Optional) Map of attributes of the thing.
* `thing_type_name` - (Optional) The thing type name.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `default_client_id` - The default client ID.
* `version` - The current version of the thing record in the registry.
* `arn` - The ARN of the thing.

## Import

```bash
ytofu import aws_iot_thing.example example
```
