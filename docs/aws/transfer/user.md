# Transfer User

Create Transfer Family users using ytofu YAML.

## S3 User

```yaml
resource:
  aws_transfer_user:
    example:
      server_id: ${aws_transfer_server.example.id}
      user_name: example
      role: ${aws_iam_role.transfer.arn}
      home_directory: /${aws_s3_bucket.example.id}
      tags:
        Name: example
```

## With Scoped Home Directory

```yaml
resource:
  aws_transfer_user:
    example:
      server_id: ${aws_transfer_server.example.id}
      user_name: example
      role: ${aws_iam_role.transfer.arn}
      home_directory_type: LOGICAL
      home_directory_mappings:
        - entry: /
          target: /${aws_s3_bucket.example.id}/home/${aws_transfer_user.example.user_name}
```
