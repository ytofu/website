# Oam Sink Policy

Manage Oam Sink Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_oam_sink:
    example:
      name: ExampleSink

resource:
  aws_oam_sink_policy:
    example:
      sink_identifier: ${aws_oam_sink.example.arn}
      policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": ["oam:CreateLink", "oam:UpdateLink"] "Effect": "Allow" "Resource": "*" "Principal": { "AWS" = ["1111111111111", "222222222222"] } "Condition": { "ForAllValues:StringEquals" = { "oam:ResourceTypes" = ["AWS::CloudWatch::Metric", "AWS::Logs::LogGroup"] } } } ] }'
```
