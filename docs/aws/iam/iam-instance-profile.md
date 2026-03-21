# IAM Instance Profile

Manage IAM Instance Profile resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iam_instance_profile:
    test_profile:
      name: test_profile
      role: ${aws_iam_role.role.name}

data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - ec2.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    role:
      name: test_role
      path: /
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}
```
