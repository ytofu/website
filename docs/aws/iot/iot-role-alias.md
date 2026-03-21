# IOT Role Alias

Manage IOT Role Alias resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_iam_policy_document:
    assume_role:
      effect: Allow
      principals:
        type: Service
        identifiers: 
          - credentials.iot.amazonaws.com
      actions: 
        - "sts:AssumeRole"

resource:
  aws_iam_role:
    role:
      name: dynamodb-access-role
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

resource:
  aws_iot_role_alias:
    alias:
      alias: Thermostat-dynamodb-access-role-alias
      role_arn: ${aws_iam_role.role.arn}
```
