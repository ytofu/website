# Ssmincidents Response Plan

Manage Ssmincidents Response Plan resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ssmincidents_response_plan:
    example:
      name: name
      incident_template:
        title: title
        impact: 3
      tags:
        key: value
      depends_on: 
        - ${aws_ssmincidents_replication_set.example}
```

## Usage With All Fields

```yaml
resource:
  aws_ssmincidents_response_plan:
    example:
      name: name
      incident_template:
        title: title
        impact: 3
        dedupe_string: dedupe
        incident_tags:
          key: value
        notification_target:
          sns_topic_arn: ${aws_sns_topic.example1.arn}
        notification_target:
          sns_topic_arn: ${aws_sns_topic.example2.arn}
        summary: summary
      display_name: display name
      chat_channel: 
        - ${aws_sns_topic.topic.arn}
      engagements: 
        - "arn:aws:ssm-contacts:us-east-2:111122223333:contact/test1"
      action:
        ssm_automation:
          document_name: ${aws_ssm_document.document1.name}
          role_arn: ${aws_iam_role.role1.arn}
          document_version: version1
          target_account: RESPONSE_PLAN_OWNER_ACCOUNT
          parameter:
            name: key
            values: 
              - value1
              - value2
          parameter:
            name: foo
            values: 
              - bar
          dynamic_parameters:
            someKey: INVOLVED_RESOURCES
            anotherKey: INCIDENT_RECORD_ARN
      integration:
        pagerduty:
          name: pagerdutyIntergration
          service_id: example
          secret_id: example
      tags:
        key: value
      depends_on: 
        - ${aws_ssmincidents_replication_set.example}
```
