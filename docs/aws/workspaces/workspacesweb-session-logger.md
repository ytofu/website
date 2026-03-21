# Workspacesweb Session Logger

Manage Workspacesweb Session Logger resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: example-session-logs

data:
  aws_iam_policy_document:
    example:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - workspaces-web.amazonaws.com
        actions:
          - "s3:PutObject"
        resources: 
          - "${aws_s3_bucket.example.arn}/*"

resource:
  aws_s3_bucket_policy:
    example:
      bucket: ${aws_s3_bucket.example.id}
      policy: ${data.aws_iam_policy_document.example.json}

resource:
  aws_workspacesweb_session_logger:
    example:
      display_name: example-session-logger
      event_filter:
        all:
        log_configuration:
          s3:
            bucket: ${aws_s3_bucket.example.id}
            folder_structure: Flat
            log_file_format: Json
        depends_on: 
          - ${aws_s3_bucket_policy.example}
```

## Complete Configuration with KMS Encryption

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: example-session-logs
      force_destroy: true

data:
  aws_iam_policy_document:
    example:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - workspaces-web.amazonaws.com
        actions:
          - "s3:PutObject"
        resources:
          - ${aws_s3_bucket.example.arn}
          - "${aws_s3_bucket.example.arn}/*"

resource:
  aws_s3_bucket_policy:
    example:
      bucket: ${aws_s3_bucket.example.id}
      policy: ${data.aws_iam_policy_document.example.json}

data:
  aws_partition:
    current:

data:
  aws_caller_identity:
    current:

data:
  aws_iam_policy_document:
    kms_key_policy:
      statement:
        principals:
          type: AWS
          identifiers: 
            - "arn:${data.aws_partition.current.partition}:iam::${data.aws_caller_identity.current.account_id}:root"
        actions: 
          - "kms:*"
        resources: 
          - "*"
      statement:
        principals:
          type: Service
          identifiers: 
            - workspaces-web.amazonaws.com
        actions:
          - "kms:Encrypt"
          - "kms:GenerateDataKey*"
          - "kms:ReEncrypt*"
          - "kms:Decrypt"
        resources: 
          - "*"

resource:
  aws_kms_key:
    example:
      description: KMS key for WorkSpaces Web Session Logger
      policy: ${data.aws_iam_policy_document.kms_key_policy.json}

resource:
  aws_workspacesweb_session_logger:
    example:
      display_name: example-session-logger
      customer_managed_key: ${aws_kms_key.example.arn}
      additional_encryption_context:
        Environment: Production
        Application: WorkSpacesWeb
      event_filter:
        include: 
          - SessionStart
          - SessionEnd
      log_configuration:
        s3:
          bucket: ${aws_s3_bucket.example.id}
          bucket_owner: ${data.aws_caller_identity.current.account_id}
          folder_structure: NestedByDate
          key_prefix: workspaces-web-logs/
          log_file_format: JsonLines
      tags:
        Name: example-session-logger
        Environment: Production
      depends_on: 
        - ${aws_s3_bucket_policy.example}
        - ${aws_kms_key.example}
```
