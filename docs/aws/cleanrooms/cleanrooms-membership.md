# Cleanrooms Membership

Manage Cleanrooms Membership resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cleanrooms_membership:
    test_membership:
      collaboration_id: 1234abcd-12ab-34cd-56ef-1234567890ab
      query_log_status: DISABLED
      default_result_configuration:
        role_arn: "arn:aws:iam::123456789012:role/role-name"
        output_configuration:
          s3:
            bucket: test-bucket
            result_format: PARQUET
            key_prefix: test-prefix
      tags:
        Project: Terraform
```
