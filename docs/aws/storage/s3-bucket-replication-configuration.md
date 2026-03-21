# Resource: aws_s3_bucket_replication_configuration

Provides an independent configuration resource for S3 bucket [replication configuration](http://docs.aws.amazon.com/AmazonS3/latest/dev/crr.html).

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
  aws_iam_role:
    replication:
      name: tf-iam-role-replication-12345
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

  aws_iam_policy:
    replication:
      name: tf-iam-role-policy-replication-12345
      policy: ${data.aws_iam_policy_document.replication.json}

  aws_iam_role_policy_attachment:
    replication:
      role: ${aws_iam_role.replication.name}
      policy_arn: ${aws_iam_policy.replication.arn}

  aws_s3_bucket:
    destination:
      bucket: tf-test-bucket-destination-12345

  aws_s3_bucket_versioning:
    destination:
      bucket: ${aws_s3_bucket.destination.id}
      versioning_configuration:
        status: Enabled

  aws_s3_bucket:
    source:
      bucket: tf-test-bucket-source-12345

  aws_s3_bucket_acl:
    source_bucket_acl:
      bucket: ${aws_s3_bucket.source.id}
      acl: private

  aws_s3_bucket_versioning:
    source:
      bucket: ${aws_s3_bucket.source.id}
      versioning_configuration:
        status: Enabled

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
          storage_class: STANDARD```

## Bi-Directional Replication

```yaml
resource:
  aws_s3_bucket:
    east:
      bucket: tf-test-bucket-east-12345

  aws_s3_bucket_versioning:
    east:
      bucket: ${aws_s3_bucket.east.id}
      versioning_configuration:
        status: Enabled

  aws_s3_bucket:
    west:
      bucket: tf-test-bucket-west-12345

  aws_s3_bucket_versioning:
    west:
      bucket: ${aws_s3_bucket.west.id}
      versioning_configuration:
        status: Enabled

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
          storage_class: STANDARD```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `bucket` - (Required) Name of the source S3 bucket you want Amazon S3 to monitor.
* `role` - (Required) ARN of the IAM role for Amazon S3 to assume when replicating the objects.
* `rule` - (Required) List of configuration blocks describing the rules managing the replication. [See below](#rule).
* `token` - (Optional) Token to allow replication to be enabled on an Object Lock-enabled bucket. You must contact AWS support for the bucket's "Object Lock token".
For more details, see [Using S3 Object Lock with replication](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lock-managing.html#object-lock-managing-replication).

### rule

The `rule` configuration block supports the following arguments:

* `delete_marker_replication` - (Optional) Whether delete markers are replicated. This argument is only valid with V2 replication configurations (i.e., when `filter` is used)[documented below](#delete_marker_replication).
* `destination` - (Required) Specifies the destination for the rule. [See below](#destination).
* `existing_object_replication` - (Optional) Replicate existing objects in the source bucket according to the rule configurations. [See below](#existing_object_replication).
* `filter` - (Optional, Conflicts with `prefix`) Filter that identifies subset of objects to which the replication rule applies. [See below](#filter). If not specified, the `rule` will default to using `prefix`.
* `id` - (Optional) Unique identifier for the rule. Must be less than or equal to 255 characters in length.
* `priority` - (Optional) Priority associated with the rule. Priority should only be set if `filter` is configured. If not provided, defaults to `0`. Priority must be unique between multiple rules.
* `source_selection_criteria` - (Optional) Specifies special object selection criteria. [See below](#source_selection_criteria).
* `status` - (Required) Status of the rule. Either `"Enabled"` or `"Disabled"`. The rule is ignored if status is not "Enabled".

### delete_marker_replication

```
delete_marker_replication {
  status = "Enabled"
}
```

The `delete_marker_replication` configuration block supports the following arguments:

* `status` - (Required) Whether delete markers should be replicated. Either `"Enabled"` or `"Disabled"`.

### destination

The `destination` configuration block supports the following arguments:

* `access_control_translation` - (Optional) Configuration block that specifies the overrides to use for object owners on replication. [See below](#access_control_translation). Specify this only in a cross-account scenario (where source and destination bucket owners are not the same), and you want to change replica ownership to the AWS account that owns the destination bucket. If this is not specified in the replication configuration, the replicas are owned by same AWS account that owns the source object. Must be used in conjunction with `account` owner override configuration.
* `account` - (Optional) Account ID to specify the replica ownership. Must be used in conjunction with `access_control_translation` override configuration.
* `bucket` - (Required) ARN of the bucket where you want Amazon S3 to store the results.
* `encryption_configuration` - (Optional) Configuration block that provides information about encryption. [See below](#encryption_configuration). If `source_selection_criteria` is specified, you must specify this element.
* `metrics` - (Optional) Configuration block that specifies replication metrics-related settings enabling replication metrics and events. [See below](#metrics).
* `replication_time` - (Optional) Configuration block that specifies S3 Replication Time Control (S3 RTC), including whether S3 RTC is enabled and the time when all objects and operations on objects must be replicated. [See below](#replication_time). Replication Time Control must be used in conjunction with `metrics`.
* `storage_class` - (Optional) The [storage class](https://docs.aws.amazon.com/AmazonS3/latest/API/API_Destination.html#AmazonS3-Type-Destination-StorageClass) used to store the object. By default, Amazon S3 uses the storage class of the source object to create the object replica.

### access_control_translation

```
access_control_translation {
  owner = "Destination"
}
```

The `access_control_translation` configuration block supports the following arguments:

* `owner` - (Required) Specifies the replica ownership. For default and valid values, see [PUT bucket replication](https://docs.aws.amazon.com/AmazonS3/latest/API/RESTBucketPUTreplication.html) in the Amazon S3 API Reference. Valid values: `Destination`.

### encryption_configuration

```
encryption_configuration {
  replica_kms_key_id = "arn:aws:kms:us-west-2:111122223333:key/1234abcd-12ab-34cd-56ef-1234567890ab"
}
```

The `encryption_configuration` configuration block supports the following arguments:

* `replica_kms_key_id` - (Required) ID (Key ARN or Alias ARN) of the customer managed AWS KMS key stored in AWS Key Management Service (KMS) for the destination bucket.

### metrics

```
metrics {
  event_threshold {
    minutes = 15
  }
  status = "Enabled"
}
```

The `metrics` configuration block supports the following arguments:

* `event_threshold` - (Optional) Configuration block that specifies the time threshold for emitting the `s3:Replication:OperationMissedThreshold` event. [See below](#event_threshold).
* `status` - (Required) Status of the Destination Metrics. Either `"Enabled"` or `"Disabled"`.

### event_threshold

The `event_threshold` configuration block supports the following arguments:

* `minutes` - (Required) Time in minutes. Valid values: `15`.

### replication_time

```
replication_time {
  status = "Enabled"
  time {
    minutes = 15
  }
}
```

The `replication_time` configuration block supports the following arguments:

* `status` - (Required) Status of the Replication Time Control. Either `"Enabled"` or `"Disabled"`.
* `time` - (Required) Configuration block specifying the time by which replication should be complete for all objects and operations on objects. [See below](#time).

### time

The `time` configuration block supports the following arguments:

* `minutes` - (Required) Time in minutes. Valid values: `15`.

### existing_object_replication

```
existing_object_replication {
  status = "Enabled"
}
```

The `existing_object_replication` configuration block supports the following arguments:

* `status` - (Required) Whether the existing objects should be replicated. Either `"Enabled"` or `"Disabled"`.

### filter

The `filter` configuration block supports the following arguments:

* `and` - (Optional) Configuration block for specifying rule filters. This element is required only if you specify more than one filter. See [and](#and) below for more details.
* `prefix` - (Optional) Object key name prefix that identifies subset of objects to which the rule applies. Must be less than or equal to 1024 characters in length.
* `tag` - (Optional) Configuration block for specifying a tag key and value. [See below](#tag).

### and

The `and` configuration block supports the following arguments:

* `prefix` - (Optional) Object key name prefix that identifies subset of objects to which the rule applies. Must be less than or equal to 1024 characters in length.
* `tags` - (Optional, Required if `prefix` is configured) Map of tags (key and value pairs) that identifies a subset of objects to which the rule applies. The rule applies only to objects having all the tags in its tagset.

### tag

The `tag` configuration block supports the following arguments:

* `key` - (Required) Name of the object key.
* `value` - (Required) Value of the tag.

### source_selection_criteria

```
source_selection_criteria {
  replica_modifications {
    status = "Enabled"
  }
  sse_kms_encrypted_objects {
    status = "Enabled"
  }
}
```

The `source_selection_criteria` configuration block supports the following arguments:

* `replica_modifications` - (Optional) Configuration block that you can specify for selections for modifications on replicas. Amazon S3 doesn't replicate replica modifications by default. In the latest version of replication configuration (when `filter` is specified), you can specify this element and set the status to `Enabled` to replicate modifications on replicas.

* `sse_kms_encrypted_objects` - (Optional) Configuration block for filter information for the selection of Amazon S3 objects encrypted with AWS KMS. If specified, `replica_kms_key_id` in `destination` `encryption_configuration` must be specified as well.

### replica_modifications

The `replica_modifications` configuration block supports the following arguments:

* `status` - (Required) Whether the existing objects should be replicated. Either `"Enabled"` or `"Disabled"`.

### sse_kms_encrypted_objects

The `sse_kms_encrypted_objects` configuration block supports the following arguments:

* `status` - (Required) Whether the existing objects should be replicated. Either `"Enabled"` or `"Disabled"`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - S3 source bucket name.

## Import

```bash
ytofu import aws_s3_bucket_replication_configuration.replication bucket-name
```
