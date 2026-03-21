# Resource: aws_iot_billing_group

Manages an AWS IoT Billing Group.

## Basic Example

```yaml
resource:
  aws_iot_billing_group:
    example:
      name: example
      properties:
        description: This is my billing group
      tags:
        terraform: true
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name of the Billing Group.
* `properties` - (Optional) The Billing Group properties. Defined below.
* `tags` - (Optional) Key-value mapping of resource tags

### properties Reference

* `description` - (Optional) A description of the Billing Group.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The ARN of the Billing Group.
* `id` - The Billing Group ID.
* `version` - The current version of the Billing Group record in the registry.

## Import

```bash
ytofu import aws_iot_billing_group.example example
```
