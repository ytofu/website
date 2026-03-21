# Transfer Web App Customization

Manage Transfer Web App Customization resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_transfer_web_app:
    test:
      identity_provider_details:
        identity_center_config:
          instance_arn: ${data.aws_ssoadmin_instances.test.arns[0]}
          role: ${aws_iam_role.test.arn}
      web_app_units:
        provisioned: 1
      tags:
        Name: test

resource:
  aws_transfer_web_app_customization:
    test:
      web_app_id: ${aws_transfer_web_app.test.web_app_id}
      favicon_file: ${filebase64("${path.module}/favicon.png")}
      logo_file: ${filebase64("${path.module}/logo.png")}
      title: test
```
