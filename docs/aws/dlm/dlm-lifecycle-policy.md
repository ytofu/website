# DLM Lifecycle Policy

Manage DLM Lifecycle Policy resources using ytofu YAML.

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
            - dlm.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    dlm_lifecycle_role:
      name: dlm-lifecycle-role
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

data:
  aws_iam_policy_document:
    dlm_lifecycle:
      statement:
        effect: Allow
        actions:
          - "ec2:CreateSnapshot"
          - "ec2:CreateSnapshots"
          - "ec2:DeleteSnapshot"
          - "ec2:DescribeInstances"
          - "ec2:DescribeVolumes"
          - "ec2:DescribeSnapshots"
        resources: 
          - "*"
      statement:
        effect: Allow
        actions: 
          - "ec2:CreateTags"
        resources: 
          - "arn:aws:ec2:*::snapshot/*"

resource:
  aws_iam_role_policy:
    dlm_lifecycle:
      name: dlm-lifecycle-policy
      role: ${aws_iam_role.dlm_lifecycle_role.id}
      policy: ${data.aws_iam_policy_document.dlm_lifecycle.json}

resource:
  aws_dlm_lifecycle_policy:
    example:
      description: example DLM lifecycle policy
      execution_role_arn: ${aws_iam_role.dlm_lifecycle_role.arn}
      state: ENABLED
      policy_details:
        resource_types: 
          - VOLUME
        schedule:
          name: 2 weeks of daily snapshots
          create_rule:
            interval: 24
            interval_unit: HOURS
            times: 
              - "23:45"
          retain_rule:
          tags_to_add:
            SnapshotCreator: DLM
          copy_tags: false
        target_tags:
          Snapshot: true
```

## Example Cross-Region Snapshot Copy Usage

```yaml
data:
  aws_caller_identity:
    current:

data:
  aws_iam_policy_document:
    key:
      statement:
        sid: Enable IAM User Permissions
        effect: Allow
        principals:
          type: AWS
          identifiers: 
            - "arn:aws:iam::${data.aws_caller_identity.current.account_id}:root"
        actions: 
          - "kms:*"
        resources: 
          - "*"

resource:
  aws_kms_key:
    dlm_cross_region_copy_cmk:
      description: Example Alternate Region KMS Key
      policy: ${data.aws_iam_policy_document.key.json}

resource:
  aws_dlm_lifecycle_policy:
    example:
      description: example DLM lifecycle policy
      execution_role_arn: ${aws_iam_role.dlm_lifecycle_role.arn}
      state: ENABLED
      policy_details:
        resource_types: 
          - VOLUME
        schedule:
          name: 2 weeks of daily snapshots
          create_rule:
            interval: 24
            interval_unit: HOURS
            times: 
              - "23:45"
          retain_rule:
          tags_to_add:
            SnapshotCreator: DLM
          copy_tags: false
          cross_region_copy_rule:
            target: us-west-2
            encrypted: true
            cmk_arn: ${aws_kms_key.dlm_cross_region_copy_cmk.arn}
            copy_tags: true
            retain_rule:
              interval: 30
              interval_unit: DAYS
        target_tags:
          Snapshot: true
```

## Example Event Based Policy Usage

```yaml
data:
  aws_caller_identity:
    current:

resource:
  aws_dlm_lifecycle_policy:
    example:
      description: tf-acc-basic
      execution_role_arn: ${aws_iam_role.example.arn}
      policy_details:
        policy_type: EVENT_BASED_POLICY
        action:
          name: tf-acc-basic
          cross_region_copy:
            encryption_configuration:
              retain_rule:
                interval: 15
                interval_unit: MONTHS
              target: us-east-1
          event_source:
            type: MANAGED_CWE
            parameters:
              description_regex: "^.*Created for policy: policy-1234567890abcdef0.*$"
              event_type: shareSnapshot
              snapshot_owner: 
                - ${data.aws_caller_identity.current.account_id}

data:
  aws_iam_policy:
    example:
      name: AWSDataLifecycleManagerServiceRole

resource:
  aws_iam_role_policy_attachment:
    example:
      role: ${aws_iam_role.example.id}
      policy_arn: ${data.aws_iam_policy.example.arn}
```
