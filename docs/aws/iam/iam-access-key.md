# IAM Access Key

Manage IAM Access Key resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iam_access_key:
    lb:
      user: ${aws_iam_user.lb.name}
      pgp_key: "keybase:some_person_that_exists"

resource:
  aws_iam_user:
    lb:
      name: loadbalancer
      path: /system/

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

output:
  secret:
    value: ${aws_iam_access_key.lb.encrypted_secret}
```
