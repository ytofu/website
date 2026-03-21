# S3 Bucket Replication Configuration

Manage S3 Bucket Replication Configuration resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - s3.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    replication:
      name: tf-iam-role-replication-12345
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

data:
  aws_iam_policy_document:
    replication:
      statement:
        effect: Allow
        actions:
          - "s3:GetReplicationConfiguration"
          - "s3:ListBucket"
        resources: 
          - ${aws_s3_bucket.source.arn}
      statement:
        effect: Allow
        actions:
          - "s3:GetObjectVersionForReplication"
          - "s3:GetObjectVersionAcl"
          - "s3:GetObjectVersionTagging"
        resources: 
          - "${aws_s3_bucket.source.arn}/*"
      statement:
        effect: Allow
        actions:
          - "s3:ReplicateObject"
          - "s3:ReplicateDelete"
          - "s3:ReplicateTags"
        resources: 
          - "${aws_s3_bucket.destination.arn}/*"

resource:
  aws_iam_policy:
    replication:
      name: tf-iam-role-policy-replication-12345
      policy: ${data.aws_iam_policy_document.replication.json}

resource:
  aws_iam_role_policy_attachment:
    replication:
      role: ${aws_iam_role.replication.name}
      policy_arn: ${aws_iam_policy.replication.arn}

resource:
  aws_s3_bucket:
    destination:
      bucket: tf-test-bucket-destination-12345

resource:
  aws_s3_bucket_versioning:
    destination:
      bucket: ${aws_s3_bucket.destination.id}
      versioning_configuration:
        status: Enabled

resource:
  aws_s3_bucket:
    source:
      bucket: tf-test-bucket-source-12345

resource:
  aws_s3_bucket_acl:
    source_bucket_acl:
      bucket: ${aws_s3_bucket.source.id}
      acl: private

resource:
  aws_s3_bucket_versioning:
    source:
      bucket: ${aws_s3_bucket.source.id}
      versioning_configuration:
        status: Enabled

resource:
  aws_s3_bucket_replication_configuration:
    replication:
      depends_on: 
        - ${aws_s3_bucket_versioning.source}
      role: ${aws_iam_role.replication.arn}
      bucket: ${aws_s3_bucket.source.id}
      rule:
        id: examplerule
        filter:
          prefix: example
        status: Enabled
        destination:
          bucket: ${aws_s3_bucket.destination.arn}
          storage_class: STANDARD
```

## Bi-Directional Replication

```yaml
resource:
  aws_s3_bucket:
    east:
      bucket: tf-test-bucket-east-12345

resource:
  aws_s3_bucket_versioning:
    east:
      bucket: ${aws_s3_bucket.east.id}
      versioning_configuration:
        status: Enabled

resource:
  aws_s3_bucket:
    west:
      bucket: tf-test-bucket-west-12345

resource:
  aws_s3_bucket_versioning:
    west:
      bucket: ${aws_s3_bucket.west.id}
      versioning_configuration:
        status: Enabled

resource:
  aws_s3_bucket_replication_configuration:
    east_to_west:
      depends_on: 
        - ${aws_s3_bucket_versioning.east}
      role: ${aws_iam_role.east_replication.arn}
      bucket: ${aws_s3_bucket.east.id}
      rule:
        id: foobar
        filter:
          prefix: foo
        status: Enabled
        destination:
          bucket: ${aws_s3_bucket.west.arn}
          storage_class: STANDARD

resource:
  aws_s3_bucket_replication_configuration:
    west_to_east:
      depends_on: 
        - ${aws_s3_bucket_versioning.west}
      role: ${aws_iam_role.west_replication.arn}
      bucket: ${aws_s3_bucket.west.id}
      rule:
        id: foobar
        filter:
          prefix: foo
        status: Enabled
        destination:
          bucket: ${aws_s3_bucket.east.arn}
          storage_class: STANDARD
```
