# Resource: aws_workspacesweb_browser_settings

ytofu resource for managing an AWS WorkSpaces Web Browser Settings resource.

## Basic Example

```yaml
resource:
  aws_workspacesweb_browser_settings:
    example:
      browser_policy: '{ "AdditionalSettings": { "DownloadsSettings": { "Behavior": "DISABLE" } } }'
```

## With All Arguments

```yaml
resource:
  aws_kms_key:
    example:
      description: KMS key for WorkSpaces Web Browser Settings
      deletion_window_in_days: 7

  aws_workspacesweb_browser_settings:
    example:
      browser_policy: '{ "chromePolicies": { "DefaultDownloadDirectory": { "value": "/home/as2-streaming-user/MyFiles/TemporaryFiles1" } } }'
      customer_managed_key: ${aws_kms_key.example.arn}
      additional_encryption_context:
        Environment: Production
      tags:
        Name: example-browser-settings```

## Argument Reference

The following arguments are required:

* `browser_policy` - (Required) Browser policy for the browser settings. This is a JSON string that defines the browser settings policy.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `additional_encryption_context` - (Optional) Additional encryption context for the browser settings.
* `customer_managed_key` - (Optional) ARN of the customer managed KMS key.
* `tags` - (Optional) Map of tags assigned to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `associated_portal_arns` - List of web portal ARNs to associate with the browser settings.
* `browser_settings_arn` - ARN of the browser settings resource.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_workspacesweb_browser_settings.example arn:aws:workspacesweb:us-west-2:123456789012:browsersettings/abcdef12345
```
