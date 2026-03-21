# VPC Endpoint Connection Notification

Manage VPC Endpoint Connection Notification resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_iam_policy_document:
    topic:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - vpce.amazonaws.com
        actions: 
          - "SNS:Publish"
        resources: 
          - "arn:aws:sns:*:*:vpce-notification-topic"

resource:
  aws_sns_topic:
    topic:
      name: vpce-notification-topic
      policy: ${data.aws_iam_policy_document.topic.json}

resource:
  aws_vpc_endpoint_service:
    foo:
      acceptance_required: false
      network_load_balancer_arns: 
        - ${aws_lb.test.arn}

resource:
  aws_vpc_endpoint_connection_notification:
    foo:
      vpc_endpoint_service_id: ${aws_vpc_endpoint_service.foo.id}
      connection_notification_arn: ${aws_sns_topic.topic.arn}
      connection_events: 
        - Accept
        - Reject
```
