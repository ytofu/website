# Resource: aws_s3vectors_vector_bucket_policy

ytofu resource for managing an Amazon S3 Vectors Vector Bucket policy.

## Basic Example

```yaml
resource:
  aws_s3vectors_vector_bucket_policy:
    example:
      vector_bucket_arn: ${aws_s3vectors_vector_bucket.example.arn}
      policy: |
        {
        "Version": "2012-10-17",
        "Id": "writePolicy",
        "Statement": [{
        "Sid": "writeStatement",
        "Effect": "Allow",
        "Principal": {
        "AWS": "123456789012"
        },
        "Action": [
        "s3vectors:PutVectors"
        ],
        "Resource": "*"
        }]
        }
```

## Argument Reference

The following arguments are required:

* `policy` - (Required) The policy document.
* `vector_bucket_arn` - (Required, Forces new resource) ARN of the vector bucket.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_s3vectors_vector_bucket_policy.example arn:aws:s3vectors:us-west-2:123456789012:bucket/example-bucket
```
