# S3 Bucket Acl

Manage S3 Bucket Acl resources using ytofu YAML.

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
