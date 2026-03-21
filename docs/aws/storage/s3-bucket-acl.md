# Resource: aws_s3_bucket_acl

Provides an S3 bucket ACL resource.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: my-tf-example-bucket

resource:
  aws_s3_bucket_ownership_controls:
    example:
      bucket: ${aws_s3_bucket.example.id}
      rule:
        object_ownership: BucketOwnerPreferred

resource:
  aws_s3_bucket_acl:
    example:
      depends_on: 
        - ${aws_s3_bucket_ownership_controls.example}
      bucket: ${aws_s3_bucket.example.id}
      acl: private
```

## With `public-read` ACL

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: my-tf-example-bucket

resource:
  aws_s3_bucket_ownership_controls:
    example:
      bucket: ${aws_s3_bucket.example.id}
      rule:
        object_ownership: BucketOwnerPreferred

resource:
  aws_s3_bucket_public_access_block:
    example:
      bucket: ${aws_s3_bucket.example.id}
      block_public_acls: false
      block_public_policy: false
      ignore_public_acls: false
      restrict_public_buckets: false

resource:
  aws_s3_bucket_acl:
    example:
      depends_on:
        - ${aws_s3_bucket_ownership_controls.example}
        - ${aws_s3_bucket_public_access_block.example}
      bucket: ${aws_s3_bucket.example.id}
      acl: public-read
```

## With Grants

```yaml
data:
  aws_canonical_user_id:
    current:

resource:
  aws_s3_bucket:
    example:
      bucket: my-tf-example-bucket

resource:
  aws_s3_bucket_ownership_controls:
    example:
      bucket: ${aws_s3_bucket.example.id}
      rule:
        object_ownership: BucketOwnerPreferred

resource:
  aws_s3_bucket_acl:
    example:
      depends_on: 
        - ${aws_s3_bucket_ownership_controls.example}
      bucket: ${aws_s3_bucket.example.id}
      access_control_policy:
        grant:
          grantee:
            id: ${data.aws_canonical_user_id.current.id}
            type: CanonicalUser
          permission: READ
        grant:
          grantee:
            type: Group
            uri: "http://acs.amazonaws.com/groups/s3/LogDelivery"
          permission: READ_ACP
        owner:
          id: ${data.aws_canonical_user_id.current.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `acl` - (Optional, either `access_control_policy` or `acl` is required) Specifies the Canned ACL to apply to the bucket. Valid values: `private`, `public-read`, `public-read-write`, `aws-exec-read`, `authenticated-read`, `bucket-owner-read`, `bucket-owner-full-control`, `log-delivery-write`. Full details are available on the [AWS documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/acl-overview.html#canned-acl).
* `access_control_policy` - (Optional, either `access_control_policy` or `acl` is required) Configuration block that sets the ACL permissions for an object per grantee. [See below](#access_control_policy).
* `bucket` - (Required, Forces new resource) Bucket to which to apply the ACL.

### access_control_policy

The `access_control_policy` configuration block supports the following arguments:

* `grant` - (Required) Set of `grant` configuration blocks. [See below](#grant).
* `owner` - (Required) Configuration block for the bucket owner's display name and ID. [See below](#owner).

### grant

The `grant` configuration block supports the following arguments:

* `grantee` - (Required) Configuration block for the person being granted permissions. [See below](#grantee).
* `permission` - (Required) Logging permissions assigned to the grantee for the bucket. Valid values: `FULL_CONTROL`, `WRITE`, `WRITE_ACP`, `READ`, `READ_ACP`. See [What permissions can I grant?](https://docs.aws.amazon.com/AmazonS3/latest/userguide/acl-overview.html#permissions) for more details about what each permission means in the context of buckets.

### owner

The `owner` configuration block supports the following arguments:

* `id` - (Required) ID of the owner.
* `display_name` - (Optional) Display name of the owner.

### grantee

The `grantee` configuration block supports the following arguments:

* `email_address` - (Optional) Email address of the grantee. See [Regions and Endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html#s3_region) for supported AWS regions where this argument can be specified.
* `id` - (Optional) Canonical user ID of the grantee.
* `type` - (Required) Type of grantee. Valid values: `CanonicalUser`, `AmazonCustomerByEmail`, `Group`.
* `uri` - (Optional) URI of the grantee group.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The `bucket`, `expected_bucket_owner` (if configured), and `acl` (if configured) separated by commas (`,`).

## Import

```bash
ytofu import aws_s3_bucket_acl.example bucket-name
```
