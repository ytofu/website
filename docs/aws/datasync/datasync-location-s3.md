# Resource: aws_datasync_location_s3

Manages an S3 Location within AWS DataSync.

## Basic Example

```yaml
resource:
  aws_datasync_location_s3:
    example:
      s3_bucket_arn: ${aws_s3_bucket.example.arn}
      subdirectory: /example/prefix
      s3_config:
        bucket_access_role_arn: ${aws_iam_role.example.arn}
```

## S3 Bucket on AWS Outposts

```yaml
resource:
  aws_datasync_location_s3:
    destination:
      agent_arns: 
        - ${aws_datasync_agent.example.arn}
      s3_bucket_arn: ${aws_s3_access_point.example.arn}
      s3_storage_class: OUTPOSTS
      subdirectory: /example/prefix
      s3_config:
        bucket_access_role_arn: ${aws_iam_role.example.arn}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `agent_arns` - (Optional) (Amazon S3 on Outposts only) Amazon Resource Name (ARN) of the DataSync agent on the Outpost.
* `s3_bucket_arn` - (Required) Amazon Resource Name (ARN) of the S3 bucket, or the Amazon S3 access point if the S3 bucket is located on an AWS Outposts resource.
* `s3_config` - (Required) Configuration block containing information for connecting to S3.
* `s3_storage_class` - (Optional) Amazon S3 storage class that you want to store your files in when this location is used as a task destination. [Valid values](https://docs.aws.amazon.com/datasync/latest/userguide/create-s3-location.html#using-storage-classes)  
* `subdirectory` - (Required) Prefix to perform actions as source or destination.
* `tags` - (Optional) Key-value pairs of resource tags to assign to the DataSync Location. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### s3_config Argument Reference

The `s3_config` configuration block supports the following arguments:

* `bucket_access_role_arn` - (Required) ARN of the IAM Role used to connect to the S3 Bucket.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Amazon Resource Name (ARN) of the DataSync Location.
* `arn` - Amazon Resource Name (ARN) of the DataSync Location.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_datasync_location_s3.example arn:aws:datasync:us-east-1:123456789012:location/loc-12345678901234567
```
