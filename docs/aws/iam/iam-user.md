# IAM User

Manage IAM User resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iam_user:
    lb:
      name: loadbalancer
      path: /system/
      tags:
        tag-key: tag-value

resource:
  aws_iam_access_key:
    lb:
      user: ${aws_iam_user.lb.name}

data:
  aws_iam_policy_document:
    lb_ro:
      statement:
        effect: Allow
        actions: 
          - "ec2:Describe*"
        resources: 
          - "*"

resource:
  aws_iam_user_policy:
    lb_ro:
      name: test
      user: ${aws_iam_user.lb.name}
      policy: ${data.aws_iam_policy_document.lb_ro.json}
```
