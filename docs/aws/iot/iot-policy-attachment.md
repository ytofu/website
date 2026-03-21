# IOT Policy Attachment

Manage IOT Policy Attachment resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_iam_policy_document:
    pubsub:
      statement:
        effect: Allow
        actions: 
          - "iot:*"
        resources: 
          - "*"

resource:
  aws_iot_policy:
    pubsub:
      name: PubSubToAnyTopic
      policy: ${data.aws_iam_policy_document.pubsub.json}

resource:
  aws_iot_certificate:
    cert:
      csr: file-content
      active: true

resource:
  aws_iot_policy_attachment:
    att:
      policy: ${aws_iot_policy.pubsub.name}
      target: ${aws_iot_certificate.cert.arn}
```
