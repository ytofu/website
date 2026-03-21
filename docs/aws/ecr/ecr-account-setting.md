# ECR Account Setting

Manage ECR Account Setting resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ecr_account_setting:
    basic_scan_type_version:
      name: BASIC_SCAN_TYPE_VERSION
      value: AWS_NATIVE
```

## Configuring Blob Mounting (Cross-Repository Layer Sharing)

```yaml
resource:
  aws_ecr_account_setting:
    blob_mounting:
      name: BLOB_MOUNTING
      value: ENABLED
```

## Configuring Registry Policy Scope

```yaml
resource:
  aws_ecr_account_setting:
    registry_policy_scope:
      name: REGISTRY_POLICY_SCOPE
      value: V2
```
