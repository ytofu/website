# IOT Topic Rule

Manage IOT Topic Rule resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iot_topic_rule:
    rule:
      name: MyRule
      description: Example rule
      enabled: true
      sql: "SELECT * FROM 'topic/test'"
      sql_version: 2016-03-23
      sns:
        message_format: RAW
        role_arn: ${aws_iam_role.role.arn}
        target_arn: ${aws_sns_topic.mytopic.arn}
      error_action:
        sns:
          message_format: RAW
          role_arn: ${aws_iam_role.role.arn}
          target_arn: ${aws_sns_topic.myerrortopic.arn}

resource:
  aws_sns_topic:
    mytopic:
      name: mytopic

resource:
  aws_sns_topic:
    myerrortopic:
      name: myerrortopic

data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - iot.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    myrole:
      name: myrole
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

data:
  aws_iam_policy_document:
    mypolicy:
      statement:
        effect: Allow
        actions: 
          - "sns:Publish"
        resources: 
          - ${aws_sns_topic.mytopic.arn}

resource:
  aws_iam_role_policy:
    mypolicy:
      name: mypolicy
      role: ${aws_iam_role.myrole.id}
      policy: ${data.aws_iam_policy_document.mypolicy.json}
```
