# Quicksight Data Source

Manage Quicksight Data Source resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_quicksight_data_source:
    default:
      data_source_id: example-id
      name: My Cool Data in S3
      parameters:
        s3:
          manifest_file_location:
            bucket: my-bucket
            key: path/to/manifest.json
      type: S3
```

## S3 Data Source with IAM Role ARN

```yaml
data:
  aws_caller_identity:
    current:

data:
  aws_partition:
    current:

data:
  aws_region:
    current:

resource:
  aws_s3_bucket:
    example:

resource:
  aws_s3_object:
    example:
      bucket: ${aws_s3_bucket.example.bucket}
      key: manifest.json
      content: '{ "fileLocations": [ { "URIPrefixes": [ "https://${aws_s3_bucket.example.id}.s3-${data.aws_region.current.region}.${data.aws_partition.current.dns_suffix}" ] } ] "globalUploadSettings": { "format": "CSV" "delimiter": "," "textqualifier": "\"" "containsHeader": true } }'

resource:
  aws_iam_role:
    example:
      name: example
      assume_role_policy: '{ "Version": "2012-10-17", "Statement": [ { "Action": "sts:AssumeRole" "Effect": "Allow" "Principal": { "Service": "quicksight.amazonaws.com" } "Condition": { "StringEquals": { "aws:SourceAccount" = data.aws_caller_identity.current.account_id } } } ] }'

resource:
  aws_iam_policy:
    example:
      name: example
      description: Policy to allow QuickSight access to S3 bucket
      policy: '{ "Version": "2012-10-17", "Statement": [ { "Action": ["s3:GetObject"], "Effect": "Allow", "Resource": "${aws_s3_bucket.example.arn}/${aws_s3_object.example.key}" }, { "Action": ["s3:ListBucket"], "Effect": "Allow", "Resource": aws_s3_bucket.example.arn } ] }'

resource:
  aws_iam_role_policy_attachment:
    example:
      policy_arn: ${aws_iam_policy.example.arn}
      role: ${aws_iam_role.example.name}

resource:
  aws_quicksight_data_source:
    example:
      data_source_id: example-id
      name: manifest in S3
      parameters:
        s3:
          manifest_file_location:
            bucket: ${aws_s3_bucket.example.bucket}
            key: ${aws_s3_object.example.key}
          role_arn: ${aws_iam_role.example.arn}
      type: S3
```
