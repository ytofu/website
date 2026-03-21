# Kendra Query Suggestions Block List

Manage Kendra Query Suggestions Block List resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_kendra_query_suggestions_block_list:
    example:
      index_id: ${aws_kendra_index.example.id}
      name: Example
      role_arn: ${aws_iam_role.example.arn}
      source_s3_path:
        bucket: ${aws_s3_bucket.example.id}
        key: example/suggestions.txt
      tags:
        Name: Example Kendra Index
```
