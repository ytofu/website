# Kendra Thesaurus

Manage Kendra Thesaurus resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_kendra_thesaurus:
    example:
      index_id: ${aws_kendra_index.example.id}
      name: Example
      role_arn: ${aws_iam_role.example.arn}
      source_s3_path:
        bucket: ${aws_s3_bucket.example.id}
        key: ${aws_s3_object.example.key}
      tags:
        Name: Example Kendra Thesaurus
```
