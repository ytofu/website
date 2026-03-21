# RDS Export Task

Manage RDS Export Task resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_rds_export_task:
    example:
      export_task_identifier: example
      source_arn: ${aws_db_snapshot.example.db_snapshot_arn}
      s3_bucket_name: ${aws_s3_bucket.example.id}
      iam_role_arn: ${aws_iam_role.example.arn}
      kms_key_id: ${aws_kms_key.example.arn}
```

## Complete Usage

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: example
      force_destroy: true

resource:
  aws_s3_bucket_acl:
    example:
      bucket: ${aws_s3_bucket.example.id}
      acl: private

resource:
  aws_iam_role:
    example:
      name: example
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": "sts:AssumeRole" "Effect": "Allow" "Sid": "" "Principal": { "Service": "export.rds.amazonaws.com" } }, ] }'

data:
  aws_iam_policy_document:
    example:
      statement:
        actions:
          - "s3:ListAllMyBuckets"
        resources:
          - "*"
      statement:
        actions:
          - "s3:GetBucketLocation"
          - "s3:ListBucket"
        resources:
          - ${aws_s3_bucket.example.arn}
      statement:
        actions:
          - "s3:GetObject"
          - "s3:PutObject"
          - "s3:DeleteObject"
        resources:
          - "${aws_s3_bucket.example.arn}/*"

resource:
  aws_iam_policy:
    example:
      name: example
      policy: ${data.aws_iam_policy_document.example.json}

resource:
  aws_iam_role_policy_attachment:
    example:
      role: ${aws_iam_role.example.name}
      policy_arn: ${aws_iam_policy.example.arn}

resource:
  aws_kms_key:
    example:
      deletion_window_in_days: 10

resource:
  aws_db_instance:
    example:
      identifier: example
      allocated_storage: 10
      db_name: test
      engine: mysql
      engine_version: 5.7
      instance_class: db.t3.micro
      username: foo
      password: foobarbaz
      parameter_group_name: default.mysql5.7
      skip_final_snapshot: true

resource:
  aws_db_snapshot:
    example:
      db_instance_identifier: ${aws_db_instance.example.identifier}
      db_snapshot_identifier: example

resource:
  aws_rds_export_task:
    example:
      export_task_identifier: example
      source_arn: ${aws_db_snapshot.example.db_snapshot_arn}
      s3_bucket_name: ${aws_s3_bucket.example.id}
      iam_role_arn: ${aws_iam_role.example.arn}
      kms_key_id: ${aws_kms_key.example.arn}
      export_only: 
        - database
      s3_prefix: my_prefix/example
```
