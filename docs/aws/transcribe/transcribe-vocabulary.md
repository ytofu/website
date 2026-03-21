# Resource: aws_transcribe_vocabulary

ytofu resource for managing an AWS Transcribe Vocabulary.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: example-vocab-123
      force_destroy: true

  aws_s3_object:
    object:
      bucket: ${aws_s3_bucket.example.id}
      key: transcribe/test1.txt
      source: test.txt

  aws_transcribe_vocabulary:
    example:
      vocabulary_name: example
      language_code: en-US
      vocabulary_file_uri: "s3://${aws_s3_bucket.example.id}/${aws_s3_object.object.key}"
      tags:
        tag1: value1
        tag2: value3
      depends_on:
        - ${aws_s3_object.object}```

## Argument Reference

The following arguments are required:

* `language_code` - (Required) The language code you selected for your vocabulary.
* `vocabulary_name` - (Required) The name of the Vocabulary.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `phrases` - (Optional) - A list of terms to include in the vocabulary. Conflicts with `vocabulary_file_uri`
* `vocabulary_file_uri` - (Optional) The Amazon S3 location (URI) of the text file that contains your custom vocabulary. Conflicts wth `phrases`.
* `tags` - (Optional) A map of tags to assign to the Vocabulary. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Name of the Vocabulary.
* `arn` - ARN of the Vocabulary.
* `download_uri` - Generated download URI.

## Timeouts

Configuration options:

* `create` - (Default `30m`)
* `update` - (Default `30m`)
* `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_transcribe_vocabulary.example example-name
```
