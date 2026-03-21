# Resource: aws_chime_voice_connector

Enables you to connect your phone system to the telephone network at a substantial cost savings by using SIP trunking.

## Basic Example

```yaml
resource:
  aws_chime_voice_connector:
    test:
      name: connector-test-1
      require_encryption: true
      aws_region: us-east-1
```

## Argument Reference

The following arguments are required:

* `name` - (Required) The name of the Amazon Chime Voice Connector.
* `require_encryption` - (Required) When enabled, requires encryption for the Amazon Chime Voice Connector.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `aws_region` - (Optional) The AWS Region in which the Amazon Chime Voice Connector is created. Default value: `us-east-1`
* `tags` - (Optional) Key-value mapping of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN (Amazon Resource Name) of the Amazon Chime Voice Connector.
* `outbound_host_name` - The outbound host name for the Amazon Chime Voice Connector.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_chime_voice_connector.test example
```
