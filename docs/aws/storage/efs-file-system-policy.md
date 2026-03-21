# EFS File System Policy

Manage EFS File System Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_efs_file_system:
    fs:
      creation_token: my-product

data:
  aws_iam_policy_document:
    policy:
      statement:
        sid: ExampleStatement01
        effect: Allow
        principals:
          type: AWS
          identifiers: 
            - "*"
        actions:
          - "elasticfilesystem:ClientMount"
          - "elasticfilesystem:ClientWrite"
        resources: 
          - ${aws_efs_file_system.fs.arn}
        condition:
          test: Bool
          values: 
            - true

resource:
  aws_efs_file_system_policy:
    policy:
      file_system_id: ${aws_efs_file_system.fs.id}
      policy: ${data.aws_iam_policy_document.policy.json}
```
