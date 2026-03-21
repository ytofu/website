# KMS Grant

Manage KMS Grant resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_kms_key:
    a:

data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: lambda.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    a:
      name: iam-role-for-grant
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

resource:
  aws_kms_grant:
    a:
      name: my-grant
      key_id: ${aws_kms_key.a.key_id}
      grantee_principal: ${aws_iam_role.a.arn}
      operations: 
        - Encrypt
        - Decrypt
        - GenerateDataKey
      constraints:
        encryption_context_equals:
          Department: Finance
```
