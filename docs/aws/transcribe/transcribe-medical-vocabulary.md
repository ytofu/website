# Transcribe Medical Vocabulary

Manage Transcribe Medical Vocabulary resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: example-medical-vocab-123
      force_destroy: true

resource:
  aws_s3_object:
    object:
      bucket: ${aws_s3_bucket.example.id}
      key: transcribe/test1.txt
      source: test.txt

resource:
  aws_transcribe_medical_vocabulary:
    example:
      vocabulary_name: example
      language_code: en-US
      vocabulary_file_uri: "s3://${aws_s3_bucket.example.id}/${aws_s3_object.object.key}"
      tags:
        tag1: value1
        tag2: value3
      depends_on:
        - ${aws_s3_object.object}
```
