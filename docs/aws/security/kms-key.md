# KMS Key

Manage KMS Key resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

resource:
  aws_kms_key:
    example:
      description: An example symmetric encryption KMS key
      enable_key_rotation: true
      deletion_window_in_days: 20
      policy: '{ "Version": "2012-10-17" "Id": "key-default-1" "Statement": [ { "Sid": "Enable IAM User Permissions" "Effect": "Allow" "Principal": { "AWS": "arn:aws:iam::${data.aws_caller_identity.current.account_id}:root" }, "Action": "kms:*" "Resource": "*" }, { "Sid": "Allow administration of the key" "Effect": "Allow" "Principal": { "AWS": "arn:aws:iam::${data.aws_caller_identity.current.account_id}:user/Alice" }, "Action": [ "kms:ReplicateKey", "kms:Create*", "kms:Describe*", "kms:Enable*", "kms:List*", "kms:Put*", "kms:Update*", "kms:Revoke*", "kms:Disable*", "kms:Get*", "kms:Delete*", "kms:ScheduleKeyDeletion", "kms:CancelKeyDeletion" ], "Resource": "*" }, { "Sid": "Allow use of the key" "Effect": "Allow" "Principal": { "AWS": "arn:aws:iam::${data.aws_caller_identity.current.account_id}:user/Bob" }, "Action": [ "kms:DescribeKey", "kms:Encrypt", "kms:Decrypt", "kms:ReEncrypt*", "kms:GenerateDataKey", "kms:GenerateDataKeyWithoutPlaintext" ], "Resource": "*" } ] }'
```

## Symmetric Encryption KMS Key With Standalone Policy Resource

```yaml
data:
  aws_caller_identity:
    current:

resource:
  aws_kms_key:
    example:
      description: An example symmetric encryption KMS key
      enable_key_rotation: true
      deletion_window_in_days: 20

resource:
  aws_kms_key_policy:
    example:
      key_id: ${aws_kms_key.example.id}
      policy: '{ "Version": "2012-10-17" "Id": "key-default-1" "Statement": [ { "Sid": "Enable IAM User Permissions" "Effect": "Allow" "Principal": { "AWS": "arn:aws:iam::${data.aws_caller_identity.current.account_id}:root" }, "Action": "kms:*" "Resource": "*" } ] }'
```

## Asymmetric KMS Key

```yaml
data:
  aws_caller_identity:
    current:

resource:
  aws_kms_key:
    example:
      description: RSA-3072 asymmetric KMS key for signing and verification
      customer_master_key_spec: RSA_3072
      key_usage: SIGN_VERIFY
      enable_key_rotation: false
      policy: '{ "Version": "2012-10-17" "Id": "key-default-1" "Statement": [ { "Sid": "Enable IAM User Permissions" "Effect": "Allow" "Principal": { "AWS": "arn:aws:iam::${data.aws_caller_identity.current.account_id}:root" }, "Action": "kms:*" "Resource": "*" }, { "Sid": "Allow administration of the key" "Effect": "Allow" "Principal": { "AWS": "arn:aws:iam::${data.aws_caller_identity.current.account_id}:role/Admin" }, "Action": [ "kms:Create*", "kms:Describe*", "kms:Enable*", "kms:List*", "kms:Put*", "kms:Update*", "kms:Revoke*", "kms:Disable*", "kms:Get*", "kms:Delete*", "kms:ScheduleKeyDeletion", "kms:CancelKeyDeletion" ], "Resource": "*" }, { "Sid": "Allow use of the key" "Effect": "Allow" "Principal": { "AWS": "arn:aws:iam::${data.aws_caller_identity.current.account_id}:role/Developer" }, "Action": [ "kms:Sign", "kms:Verify", "kms:DescribeKey" ], "Resource": "*" } ] }'
```

## HMAC KMS key

```yaml
data:
  aws_caller_identity:
    current:

resource:
  aws_kms_key:
    example:
      description: HMAC_384 key for tokens
      customer_master_key_spec: HMAC_384
      key_usage: GENERATE_VERIFY_MAC
      enable_key_rotation: false
      policy: '{ "Version": "2012-10-17" "Id": "key-default-1" "Statement": [ { "Sid": "Enable IAM User Permissions" "Effect": "Allow" "Principal": { "AWS": "arn:aws:iam::${data.aws_caller_identity.current.account_id}:root" }, "Action": "kms:*" "Resource": "*" }, { "Sid": "Allow administration of the key" "Effect": "Allow" "Principal": { "AWS": "arn:aws:iam::${data.aws_caller_identity.current.account_id}:role/Admin" }, "Action": [ "kms:Create*", "kms:Describe*", "kms:Enable*", "kms:List*", "kms:Put*", "kms:Update*", "kms:Revoke*", "kms:Disable*", "kms:Get*", "kms:Delete*", "kms:ScheduleKeyDeletion", "kms:CancelKeyDeletion" ], "Resource": "*" }, { "Sid": "Allow use of the key" "Effect": "Allow" "Principal": { "AWS": "arn:aws:iam::${data.aws_caller_identity.current.account_id}:role/Developer" }, "Action": [ "kms:GenerateMac", "kms:VerifyMac", "kms:DescribeKey" ], "Resource": "*" } ] }'
```

## Multi-Region Primary Key

```yaml
data:
  aws_caller_identity:
    current:

resource:
  aws_kms_key:
    example:
      description: An example multi-Region primary key
      multi_region: true
      enable_key_rotation: true
      deletion_window_in_days: 10
      policy: '{ "Version": "2012-10-17" "Id": "key-default-1" "Statement": [ { "Sid": "Enable IAM User Permissions" "Effect": "Allow" "Principal": { "AWS": "arn:aws:iam::${data.aws_caller_identity.current.account_id}:root" }, "Action": "kms:*" "Resource": "*" }, { "Sid": "Allow administration of the key" "Effect": "Allow" "Principal": { "AWS": "arn:aws:iam::${data.aws_caller_identity.current.account_id}:user/Alice" }, "Action": [ "kms:ReplicateKey", "kms:Create*", "kms:Describe*", "kms:Enable*", "kms:List*", "kms:Put*", "kms:Update*", "kms:Revoke*", "kms:Disable*", "kms:Get*", "kms:Delete*", "kms:ScheduleKeyDeletion", "kms:CancelKeyDeletion" ], "Resource": "*" }, { "Sid": "Allow use of the key" "Effect": "Allow" "Principal": { "AWS": "arn:aws:iam::${data.aws_caller_identity.current.account_id}:user/Bob" }, "Action": [ "kms:DescribeKey", "kms:Encrypt", "kms:Decrypt", "kms:ReEncrypt*", "kms:GenerateDataKey", "kms:GenerateDataKeyWithoutPlaintext" ], "Resource": "*" } ] }'
```
