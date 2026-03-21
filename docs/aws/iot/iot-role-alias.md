# Resource: aws_iot_role_alias

Provides an IoT role alias.

## Basic Example

```yaml
data:
  aws_iam_policy_document:
    assume_role:
      effect: Allow
      principals:
        type: Service
        identifiers: 
          - credentials.iot.amazonaws.com
      actions: 
        - "sts:AssumeRole"

resource:
  aws_iam_role:
    role:
      name: dynamodb-access-role
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

  aws_iot_role_alias:
    alias:
      alias: Thermostat-dynamodb-access-role-alias
      role_arn: ${aws_iam_role.role.arn}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `alias` - (Required) The name of the role alias.
* `role_arn` - (Required) The identity of the role to which the alias refers.
* `credential_duration` - (Optional) The duration of the credential, in seconds. If you do not specify a value for this setting, the default maximum of one hour is applied. This setting can have a value from 900 seconds (15 minutes) to 43200 seconds (12 hours).
* `tags` - (Optional) Key-value mapping of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The ARN assigned by AWS to this role alias.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_iot_role_alias.example myalias
```
