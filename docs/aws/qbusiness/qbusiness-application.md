# Qbusiness Application

Manage Qbusiness Application resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_qbusiness_application:
    example:
      display_name: example-app
      iam_service_role_arn: ${aws_iam_role.example.arn}
      identity_center_instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}
      attachments_configuration:
        attachments_control_mode: ENABLED
```
