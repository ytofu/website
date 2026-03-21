# EMR Studio

Manage EMR Studio resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_emr_studio:
    example:
      auth_mode: SSO
      default_s3_location: "s3://${aws_s3_bucket.test.bucket}/test"
      engine_security_group_id: ${aws_security_group.test.id}
      name: example
      service_role: ${aws_iam_role.test.arn}
      subnet_ids: 
        - ${aws_subnet.test.id}
      user_role: ${aws_iam_role.test.arn}
      vpc_id: ${aws_vpc.test.id}
      workspace_security_group_id: ${aws_security_group.test.id}
```
