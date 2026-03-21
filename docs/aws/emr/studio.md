# EMR Studio

Create EMR Studio environments using ytofu YAML.

## Basic Studio

```yaml
resource:
  aws_emr_studio:
    example:
      auth_mode: SSO
      default_s3_location: s3://${aws_s3_bucket.example.bucket}/studio
      engine_security_group_id: ${aws_security_group.engine.id}
      name: example
      service_role: ${aws_iam_role.example.arn}
      subnet_ids:
        - ${aws_subnet.example.id}
      vpc_id: ${aws_vpc.example.id}
      workspace_security_group_id: ${aws_security_group.workspace.id}
```
