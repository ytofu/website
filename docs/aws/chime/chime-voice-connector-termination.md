# Resource: aws_chime_voice_connector_termination

Enable Termination settings to control outbound calling from your SIP infrastructure.

## Basic Example

```yaml
resource:
  aws_chime_voice_connector:
    default:
      name: vc-name-test
      require_encryption: true

  aws_chime_voice_connector_termination:
    default:
      disabled: false
      cps_limit: 1
      cidr_allow_list: 
        - 50.35.78.96/31
      calling_regions: 
        - US
        - CA
      voice_connector_id: ${aws_chime_voice_connector.default.id}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `voice_connector_id` - (Required) The Amazon Chime Voice Connector ID.
* `cidr_allow_list` - (Required) The IP addresses allowed to make calls, in CIDR format.
* `calling_regions` - (Required) The countries to which calls are allowed, in ISO 3166-1 alpha-2 format.
* `disabled` - (Optional) When termination settings are disabled, outbound calls can not be made.
* `default_phone_number` - (Optional) The default caller ID phone number.
* `cps_limit` - (Optional) The limit on calls per second. Max value based on account service quota. Default value of `1`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The Amazon Chime Voice Connector ID.

## Import

```bash
ytofu import aws_chime_voice_connector_termination.default abcdef1ghij2klmno3pqr4
```
