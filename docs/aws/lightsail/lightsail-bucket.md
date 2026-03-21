# Resource: aws_lightsail_bucket

Manages a Lightsail bucket. Use this resource to create and manage object storage buckets for storing files, images, and other data in Lightsail.

## Basic Example

```yaml
resource:
  aws_lightsail_bucket:
    example:
      name: example-bucket
      bundle_id: small_1_0
```

## Argument Reference

The following arguments are required:

* `bundle_id` - (Required) Bundle ID to use for the bucket. A bucket bundle specifies the monthly cost, storage space, and data transfer quota for a bucket. Use the [get-bucket-bundles](https://docs.aws.amazon.com/cli/latest/reference/lightsail/get-bucket-bundles.html) cli command to get a list of bundle IDs that you can specify.
* `name` - (Required) Name for the bucket.

The following arguments are optional:

* `force_delete` - (Optional) Whether to force delete non-empty buckets using `ytofu destroy`. AWS by default will not delete a bucket which is not empty, to prevent losing bucket data and affecting other resources in Lightsail. If `force_delete` is set to `true` the bucket will be deleted even when not empty.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `tags` - (Optional) Map of tags to assign to the resource. To create a key-only tag, use an empty string as the value. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Lightsail bucket.
* `availability_zone` - Availability Zone. Follows the format us-east-2a (case-sensitive).
* `created_at` - Date and time when the bucket was created.
* `id` - Name used for this bucket (matches `name`).
* `support_code` - Support code for the resource. Include this code in your email to support when you have questions about a resource in Lightsail. This code enables our support team to look up your Lightsail information more easily.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.
* `url` - URL of the bucket.

## Import

```bash
ytofu import aws_lightsail_bucket.example example-bucket
```
