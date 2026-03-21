# SSM Activation

Manage SSM Activation resources using ytofu YAML.

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
            - ssm.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    test_role:
      name: test_role
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

resource:
  aws_iam_role_policy_attachment:
    test_attach:
      role: ${aws_iam_role.test_role.name}
      policy_arn: "arn:aws:iam::aws:policy/AmazonSSMManagedInstanceCore"

resource:
  aws_ssm_activation:
    foo:
      name: test_ssm_activation
      description: Test
      iam_role: ${aws_iam_role.test_role.id}
      registration_limit: 5
      depends_on: 
        - ${aws_iam_role_policy_attachment.test_attach}
```
