# Resource: aws_cloudwatch_event_bus_policy

Provides a resource to create an EventBridge resource policy to support cross-account events.

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

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `policy` - (Required) The text of the policy. For more information about building AWS IAM policy documents with ytofu, see the [AWS IAM Policy Document Guide](https://learn.hashicorp.com/terraform/aws/iam-policy).
* `event_bus_name` - (Optional) The name of the event bus to set the permissions on.
  If you omit this, the permissions are set on the `default` event bus.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The name of the EventBridge event bus.

## Import

```bash
ytofu import aws_cloudwatch_event_bus_policy.DevAccountAccess example-event-bus
```
