# Resource: aws_iot_policy_attachment

Provides an IoT policy attachment.

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

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `policy` - (Required) The name of the policy to attach.
* `target` - (Required) The identity to which the policy is attached.

## Attribute Reference

This resource exports no additional attributes.
