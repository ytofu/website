# Cloudwatch Event Bus Policy

Manage Cloudwatch Event Bus Policy resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_iam_policy_document:
    test:
      statement:
        sid: DevAccountAccess
        effect: Allow
        actions:
          - "events:PutEvents"
        resources:
          - "arn:aws:events:eu-west-1:123456789012:event-bus/default"
        principals:
          type: AWS
          identifiers: 
            - 123456789012

resource:
  aws_cloudwatch_event_bus_policy:
    test:
      policy: ${data.aws_iam_policy_document.test.json}
      event_bus_name: ${aws_cloudwatch_event_bus.test.name}
```

## Organization Access

```yaml
data:
  aws_iam_policy_document:
    test:
      statement:
        sid: OrganizationAccess
        effect: Allow
        actions:
          - "events:DescribeRule"
          - "events:ListRules"
          - "events:ListTargetsByRule"
          - "events:ListTagsForResource"
        resources:
          - "arn:aws:events:eu-west-1:123456789012:rule/*"
          - "arn:aws:events:eu-west-1:123456789012:event-bus/default"
        principals:
          type: AWS
          identifiers: 
            - "*"
        condition:
          test: StringEquals
          values: 
            - ${aws_organizations_organization.example.id}

resource:
  aws_cloudwatch_event_bus_policy:
    test:
      policy: ${data.aws_iam_policy_document.test.json}
      event_bus_name: ${aws_cloudwatch_event_bus.test.name}
```

## Multiple Statements

```yaml
data:
  aws_iam_policy_document:
    test:
      statement:
        sid: DevAccountAccess
        effect: Allow
        actions:
          - "events:PutEvents"
        resources:
          - "arn:aws:events:eu-west-1:123456789012:event-bus/default"
        principals:
          type: AWS
          identifiers: 
            - 123456789012
      statement:
        sid: OrganizationAccess
        effect: Allow
        actions:
          - "events:DescribeRule"
          - "events:ListRules"
          - "events:ListTargetsByRule"
          - "events:ListTagsForResource"
        resources:
          - "arn:aws:events:eu-west-1:123456789012:rule/*"
          - "arn:aws:events:eu-west-1:123456789012:event-bus/default"
        principals:
          type: AWS
          identifiers: 
            - "*"
        condition:
          test: StringEquals
          values: 
            - ${aws_organizations_organization.example.id}

resource:
  aws_cloudwatch_event_bus_policy:
    test:
      policy: ${data.aws_iam_policy_document.test.json}
      event_bus_name: ${aws_cloudwatch_event_bus.test.name}
```
