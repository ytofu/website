# Resource: aws_transfer_tag

Manages an individual Transfer Family resource tag. This resource should only be used in cases where Transfer Family resources are created outside ytofu (e.g., Servers without AWS Management Console) or the tag key has the `aws:` prefix.

## Basic Example

```yaml
resource:
  aws_transfer_server:
    example:
      identity_provider_type: SERVICE_MANAGED

resource:
  aws_transfer_tag:
    zone_id:
      resource_arn: ${aws_transfer_server.example.arn}
      key: "transfer:route53HostedZoneId"
      value: /hostedzone/MyHostedZoneId

resource:
  aws_transfer_tag:
    hostname:
      resource_arn: ${aws_transfer_server.example.arn}
      key: "transfer:customHostname"
      value: example.com
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `resource_arn` - (Required) Amazon Resource Name (ARN) of the Transfer Family resource to tag.
* `key` - (Required) Tag name.
* `value` - (Required) Tag value.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Transfer Family resource identifier and key, separated by a comma (`,`)

## Import

```bash
ytofu import aws_transfer_tag.example arn:aws:transfer:us-east-1:123456789012:server/s-1234567890abcdef0,Name
```
