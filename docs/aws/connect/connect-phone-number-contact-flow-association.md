# Resource: aws_connect_phone_number_contact_flow_association

Associates a flow with a phone number claimed to an Amazon Connect instance.

## Basic Example

```yaml
resource:
  aws_connect_phone_number_contact_flow_association:
    example:
      phone_number_id: ${aws_connect_phone_number.example.id}
      instance_id: ${aws_connect_instance.example.id}
      contact_flow_id: ${aws_connect_contact_flow.example.contact_flow_id}
```

## Argument Reference

This resource supports the following arguments:

* `contact_flow_id` - (Required) Contact flow ID.
* `instance_id` - (Required) Amazon Connect instance ID.
* `phone_number_id` - (Required) Phone number ID.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_connect_phone_number_contact_flow_association.example 36727a4c-4683-4e49-880c-3347c61110a4,fa6c1691-e2eb-4487-bdb9-1aaed6268ebd,c4acdc79-395e-4280-a294-9062f56b07bb
```
