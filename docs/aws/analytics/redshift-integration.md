# Redshift Integration

Manage Redshift Integration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_dynamodb_table:
    example:
      name: dynamodb-table-example
      read_capacity: 1
      write_capacity: 1
      hash_key: example
      attribute:
        name: example
        type: S
      point_in_time_recovery:
        enabled: true

resource:
  aws_redshiftserverless_namespace:
    example:
      namespace_name: redshift-example

resource:
  aws_redshiftserverless_workgroup:
    example:
      namespace_name: ${aws_redshiftserverless_namespace.example.namespace_name}
      workgroup_name: example-workgroup
      base_capacity: 8
      publicly_accessible: false
      subnet_ids: 
        - ${aws_subnet.example1.id}
        - ${aws_subnet.example2.id}
        - ${aws_subnet.example3.id}
      config_parameter:
        parameter_key: enable_case_sensitive_identifier
        parameter_value: true

resource:
  aws_redshift_integration:
    example:
      integration_name: example
      source_arn: ${aws_dynamodb_table.example.arn}
      target_arn: ${aws_redshiftserverless_namespace.example.arn}
```

## Use own KMS key

```yaml
data:
  aws_caller_identity:
    current:

resource:
  aws_kms_key:
    example:
      description: example
      deletion_window_in_days: 10

resource:
  aws_kms_key_policy:
    example:
      key_id: ${aws_kms_key.example.id}
      policy: '{ "Version": "2008-10-17" "Statement": [ { "Effect": "Allow" "Principal": { "AWS": "arn:aws:iam::${data.aws_caller_identity.current.account_id}:root" } "Action": "kms:*" "Resource": "*" }, { "Effect": "Allow" "Principal": { "Service": "redshift.amazonaws.com" } "Action": [ "kms:Decrypt", "kms:CreateGrant" ] "Resource": "*" "Condition": { "StringEquals": { "aws:SourceAccount" = data.aws_caller_identity.current.account_id } "ArnEquals": { "aws:SourceArn" = "arn:aws:redshift:*:${data.aws_caller_identity.current.account_id}:integration:*" } } } ] }'

resource:
  aws_redshift_integration:
    example:
      integration_name: example
      source_arn: ${aws_dynamodb_table.example.arn}
      target_arn: ${aws_redshiftserverless_namespace.example.arn}
      kms_key_id: ${aws_kms_key.example.arn}
      additional_encryption_context: 
```
