# Kendra Faq

Manage Kendra Faq resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_kendra_faq:
    example:
      index_id: ${aws_kendra_index.example.id}
      name: Example
      role_arn: ${aws_iam_role.example.arn}
      s3_path:
        bucket: ${aws_s3_bucket.example.id}
        key: ${aws_s3_object.example.key}
      tags:
        Name: Example Kendra Faq
```

## With File Format

```yaml
resource:
  aws_kendra_faq:
    example:
      index_id: ${aws_kendra_index.example.id}
      name: Example
      file_format: CSV
      role_arn: ${aws_iam_role.example.arn}
      s3_path:
        bucket: ${aws_s3_bucket.example.id}
        key: ${aws_s3_object.example.key}
```

## With Language Code

```yaml
resource:
  aws_kendra_faq:
    example:
      index_id: ${aws_kendra_index.example.id}
      name: Example
      language_code: en
      role_arn: ${aws_iam_role.example.arn}
      s3_path:
        bucket: ${aws_s3_bucket.example.id}
        key: ${aws_s3_object.example.key}
```
