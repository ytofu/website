# IOT Policy

Manage IOT Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iot_policy:
    pubsub:
      name: PubSubToAnyTopic
      policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": [ "iot:*", ] "Effect": "Allow" "Resource": "*" }, ] }'
```
