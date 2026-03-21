# Comprehend Entity Recognizer

Manage Comprehend Entity Recognizer resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_comprehend_entity_recognizer:
    example:
      name: example
      data_access_role_arn: ${aws_iam_role.example.arn}
      language_code: en
      input_data_config:
        entity_types:
          type: ENTITY_1
        entity_types:
          type: ENTITY_2
        documents:
          s3_uri: "s3://${aws_s3_bucket.documents.bucket}/${aws_s3_object.documents.key}"
        entity_list:
          s3_uri: "s3://${aws_s3_bucket.entities.bucket}/${aws_s3_object.entities.key}"
      depends_on:
        - ${aws_iam_role_policy.example}

resource:
  aws_s3_object:
    documents:

resource:
  aws_s3_object:
    entities:
```
