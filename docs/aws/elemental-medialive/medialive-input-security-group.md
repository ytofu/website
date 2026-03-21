# Resource: aws_medialive_input_security_group

ytofu resource for managing an AWS MediaLive InputSecurityGroup.

## Basic Example

```yaml
resource:
  aws_medialive_input_security_group:
    example:
      whitelist_rules:
        cidr: 10.0.0.8/32
      tags:
        ENVIRONMENT: prod
```

## Argument Reference

The following arguments are required:

* `whitelist_rules` - (Required) Whitelist rules. See [Whitelist Rules](#whitelist-rules) for more details.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `tags` - (Optional) A map of tags to assign to the InputSecurityGroup. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### Whitelist Rules

* `cidr` (Required) - The IPv4 CIDR that's whitelisted.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - InputSecurityGroup Id.
* `arn` - ARN of the InputSecurityGroup.
* `inputs` - The list of inputs currently using this InputSecurityGroup.

## Timeouts

Configuration options:

* `create` - (Default `5m`)
* `update` - (Default `5m`)
* `delete` - (Default `5m`)

## Import

```bash
ytofu import aws_medialive_input_security_group.example 123456
```
