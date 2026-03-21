# RDS Integration

Manage RDS Integration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_redshiftserverless_namespace:
    example:
      namespace_name: redshift-example

resource:
  aws_redshiftserverless_workgroup:
    example:
      namespace_name: ${aws_redshiftserverless_namespace.example.namespace_name}
      workgroup_name: example-workspace
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
  aws_rds_integration:
    example:
      integration_name: example
      source_arn: ${aws_rds_cluster.example.arn}
      target_arn: ${aws_redshiftserverless_namespace.example.arn}
      lifecycle:
        ignore_changes:
          - kms_key_id
```

## Use own KMS key

```yaml
data:
  aws_caller_identity:
    current:

resource:
  aws_kms_key:
    example:
      deletion_window_in_days: 10
      policy: ${data.aws_iam_policy_document.key_policy.json}

data:
  aws_iam_policy_document:
    key_policy:
      statement:
        actions: 
          - "kms:*"
        resources: 
          - "*"
        principals:
          type: AWS
          identifiers: 
            - "arn:aws:iam::${data.aws_caller_identity.current.account_id}:root"
      statement:
        actions: 
          - "kms:CreateGrant"
        resources: 
          - "*"
        principals:
          type: Service
          identifiers: 
            - redshift.amazonaws.com

resource:
  aws_rds_integration:
    example:
      integration_name: example
      source_arn: ${aws_rds_cluster.example.arn}
      target_arn: ${aws_redshiftserverless_namespace.example.arn}
      kms_key_id: ${aws_kms_key.example.arn}
      additional_encryption_context: 
```
