# Redshift Idc Application

Manage Redshift Idc Application resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_redshift_idc_application:
    example:
      iam_role_arn: ${aws_iam_role.example.arn}
      idc_display_name: example
      idc_instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}
      identity_namespace: example
      redshift_idc_application_name: example
```
