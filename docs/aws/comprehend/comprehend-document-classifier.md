# Comprehend Document Classifier

Manage Comprehend Document Classifier resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_comprehend_document_classifier:
    example:
      name: example
      data_access_role_arn: ${aws_iam_role.example.arn}
      language_code: en
      input_data_config:
        s3_uri: "s3://${aws_s3_bucket.test.bucket}/${aws_s3_object.documents.key}"
      depends_on:
        - ${aws_iam_role_policy.example}

resource:
  aws_s3_object:
    documents:

resource:
  aws_s3_object:
    entities:
```
