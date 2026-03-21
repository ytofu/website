# Resource: aws_s3control_multi_region_access_point_policy

Provides a resource to manage an S3 Multi-Region Access Point access control policy.

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

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `account_id` - (Optional) The AWS account ID for the owner of the Multi-Region Access Point. Defaults to automatically determined account ID of the ytofu AWS provider.
* `details` - (Required) A configuration block containing details about the policy for the Multi-Region Access Point. See [Details Configuration Block](#details-configuration) below for more details

### Details Configuration

The `details` block supports the following:

* `name` - (Required) The name of the Multi-Region Access Point.
* `policy` - (Required) A valid JSON document that specifies the policy that you want to associate with this Multi-Region Access Point. Once applied, the policy can be edited, but not deleted. For more information, see the documentation on [Multi-Region Access Point Permissions](https://docs.aws.amazon.com/AmazonS3/latest/userguide/MultiRegionAccessPointPermissions.html).

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `established` - The last established policy for the Multi-Region Access Point.
* `id` - The AWS account ID and access point name separated by a colon (`:`).
* `proposed` - The proposed policy for the Multi-Region Access Point.

## Timeouts

Configuration options:

* `create` - (Default `15m`)
* `update` - (Default `15m`)

## Import

```bash
ytofu import aws_s3control_multi_region_access_point_policy.example 123456789012:example
```
