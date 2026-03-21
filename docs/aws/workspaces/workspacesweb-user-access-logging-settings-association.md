# Resource: aws_workspacesweb_user_access_logging_settings_association

ytofu resource for managing an AWS WorkSpaces Web User Access Logging Settings Association.

## Basic Example

```yaml
resource:
  aws_workspacesweb_portal:
    example:
      display_name: example

  aws_kinesis_stream:
    example:
      name: amazon-workspaces-web-example
      shard_count: 1

  aws_workspacesweb_user_access_logging_settings:
    example:
      kinesis_stream_arn: ${aws_kinesis_stream.example.arn}

  aws_workspacesweb_user_access_logging_settings_association:
    example:
      user_access_logging_settings_arn: ${aws_workspacesweb_user_access_logging_settings.example.user_access_logging_settings_arn}
      portal_arn: ${aws_workspacesweb_portal.example.portal_arn}```

## Argument Reference

The following arguments are required:

* `user_access_logging_settings_arn` - (Required) ARN of the user access logging settings to associate with the portal. Forces replacement if changed.
* `portal_arn` - (Required) ARN of the portal to associate with the user access logging settings. Forces replacement if changed.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports no additional attributes.
