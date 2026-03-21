# Lexv2models Bot

Manage Lexv2models Bot resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lexv2models_bot:
    example:
      name: example
      description: Example description
      data_privacy:
        child_directed: false
      idle_session_ttl_in_seconds: 60
      role_arn: ${aws_iam_role.example.arn}
      type: Bot
      tags:
        foo: bar

resource:
  aws_iam_role:
    example:
      name: example
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": "sts:AssumeRole" "Effect": "Allow" "Sid": "" "Principal": { "Service": "lexv2.amazonaws.com" } }, ] }'
      tags:
        created_by: aws
```
