# ECS Cluster

Manage ECS Cluster resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ecs_cluster:
    foo:
      name: white-hart
      setting:
        name: containerInsights
        value: enabled
```

## Execute Command Configuration with Override Logging

```yaml
resource:
  aws_kms_key:
    example:
      description: example
      deletion_window_in_days: 7

resource:
  aws_cloudwatch_log_group:
    example:
      name: example

resource:
  aws_ecs_cluster:
    test:
      name: example
      configuration:
        execute_command_configuration:
          kms_key_id: ${aws_kms_key.example.arn}
          logging: OVERRIDE
          log_configuration:
            cloud_watch_encryption_enabled: true
            cloud_watch_log_group_name: ${aws_cloudwatch_log_group.example.name}
```

## Fargate Ephemeral Storage Encryption with Customer-Managed KMS Key

```yaml
data:
  aws_caller_identity:
    current:

resource:
  aws_kms_key:
    example:
      description: example
      deletion_window_in_days: 7

resource:
  aws_kms_key_policy:
    example:
      key_id: ${aws_kms_key.example.id}
      policy: '{ "Id": "ECSClusterFargatePolicy" "Statement": [ { "Sid": "Enable IAM User Permissions" "Effect": "Allow" "Principal": { "AWS" : "*" } "Action": "kms:*" "Resource": "*" }, { "Sid": "Allow generate data key access for Fargate tasks." "Effect": "Allow" "Principal": { "Service": "fargate.amazonaws.com" } "Action": [ "kms:GenerateDataKeyWithoutPlaintext" ] "Condition": { "StringEquals": { "kms:EncryptionContext:aws:ecs:clusterAccount" = [ data.aws_caller_identity.current.account_id ] "kms:EncryptionContext:aws:ecs:clusterName" = [ "example" ] } } "Resource": "*" }, { "Sid": "Allow grant creation permission for Fargate tasks." "Effect": "Allow" "Principal": { "Service": "fargate.amazonaws.com" } "Action": [ "kms:CreateGrant" ] "Condition": { "StringEquals": { "kms:EncryptionContext:aws:ecs:clusterAccount" = [ data.aws_caller_identity.current.account_id ] "kms:EncryptionContext:aws:ecs:clusterName" = [ "example" ] } "ForAllValues:StringEquals" = { "kms:GrantOperations" = [ "Decrypt" ] } } "Resource": "*" } ] "Version": "2012-10-17" }'

resource:
  aws_ecs_cluster:
    test:
      name: example
      configuration:
        managed_storage_configuration:
          fargate_ephemeral_storage_kms_key_id: ${aws_kms_key.example.arn}
      depends_on:
        - ${aws_kms_key_policy.example}
```
