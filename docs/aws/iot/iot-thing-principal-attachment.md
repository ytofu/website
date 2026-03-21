# Resource: aws_iot_thing_principal_attachment

Attaches Principal to AWS IoT Thing.

## Basic Example

```yaml
resource:
  aws_iot_thing:
    example:
      name: example

resource:
  aws_iot_certificate:
    cert:
      csr: file-content
      active: true

resource:
  aws_iot_thing_principal_attachment:
    att:
      principal: ${aws_iot_certificate.cert.arn}
      thing: ${aws_iot_thing.example.name}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `principal` - (Required) The AWS IoT Certificate ARN or Amazon Cognito Identity ID.
* `thing` - (Required) The name of the thing.
* `thing_principal_type` - (Optional) The type of relationship to specify when attaching a principal to a thing. Valid values are `EXCLUSIVE_THING` (the thing will be the only one attached to the principal) or `NON_EXCLUSIVE_THING` (multiple things can be attached to the principal). Defaults to `NON_EXCLUSIVE_THING`.

## Attribute Reference

This resource exports no additional attributes.
