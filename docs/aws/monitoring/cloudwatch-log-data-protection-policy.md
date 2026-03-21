# Resource: aws_cloudwatch_log_data_protection_policy

Provides a CloudWatch Log Data Protection Policy resource.

## Basic Example

```yaml
resource:
  aws_cloudwatch_log_group:
    example:
      name: example

resource:
  aws_s3_bucket:
    example:
      bucket: example

resource:
  aws_cloudwatch_log_data_protection_policy:
    example:
      log_group_name: ${aws_cloudwatch_log_group.example.name}
      policy_document: '{ "Name": "Example" "Version": "2021-06-01" "Statement": [ { "Sid": "Audit" "DataIdentifier": ["arn:aws:dataprotection::aws:data-identifier/EmailAddress"] "Operation": { "Audit": { "FindingsDestination": { "S3": { "Bucket": aws_s3_bucket.example.bucket } } } } }, { "Sid": "Redact" "DataIdentifier": ["arn:aws:dataprotection::aws:data-identifier/EmailAddress"] "Operation": { "Deidentify": { "MaskConfig": {} } } } ] }'
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `log_group_name` - (Required) The name of the log group under which the log stream is to be created.
* `policy_document` - (Required) Specifies the data protection policy in JSON. Read more at [Data protection policy syntax](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/mask-sensitive-log-data-start.html#mask-sensitive-log-data-policysyntax).

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_cloudwatch_log_data_protection_policy.example my-log-group
```
