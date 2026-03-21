# Auditmanager Assessment

Manage Auditmanager Assessment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_auditmanager_assessment:
    test:
      name: example
      assessment_reports_destination:
        destination: "s3://${aws_s3_bucket.test.id}"
        destination_type: S3
      framework_id: ${aws_auditmanager_framework.test.id}
      roles:
        role_arn: ${aws_iam_role.test.arn}
        role_type: PROCESS_OWNER
      scope:
        aws_accounts:
          id: ${data.aws_caller_identity.current.account_id}
        aws_services:
          service_name: S3
```
