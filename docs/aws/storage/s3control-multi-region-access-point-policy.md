# S3control Multi Region Access Point Policy

Manage S3control Multi Region Access Point Policy resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

data:
  aws_partition:
    current:

resource:
  aws_s3_bucket:
    foo_bucket:
      bucket: example-bucket-foo

resource:
  aws_s3control_multi_region_access_point:
    example:
      details:
        name: example
        region:
          bucket: ${aws_s3_bucket.foo_bucket.id}

resource:
  aws_s3control_multi_region_access_point_policy:
    example:
      details:
        name: example-value
        policy: '{ "Version" : "2012-10-17", "Statement" : [ { "Sid" : "Example", "Effect" : "Allow", "Principal" : { "AWS" : data.aws_caller_identity.current.account_id }, "Action" : ["s3:GetObject", "s3:PutObject"], "Resource" : "arn:${data.aws_partition.current.partition}:s3::${data.aws_caller_identity.current.account_id}:accesspoint/${aws_s3control_multi_region_access_point.example.alias}/object/*" } ] }'
```
