# Appconfig Extension

Manage Appconfig Extension resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sns_topic:
    test:
      name: test

data:
  aws_iam_policy_document:
    test:
      statement:
        actions: 
          - "sts:AssumeRole"
        principals:
          type: Service
          identifiers: 
            - appconfig.amazonaws.com

resource:
  aws_iam_role:
    test:
      name: test
      assume_role_policy: ${data.aws_iam_policy_document.test.json}

resource:
  aws_appconfig_extension:
    test:
      name: test
      description: test description
      action_point:
        point: ON_DEPLOYMENT_COMPLETE
        action:
          name: test
          role_arn: ${aws_iam_role.test.arn}
          uri: ${aws_sns_topic.test.arn}
      tags:
        Type: AppConfig Extension
```
