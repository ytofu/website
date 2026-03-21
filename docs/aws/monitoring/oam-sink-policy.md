# Resource: aws_oam_sink_policy

ytofu resource for managing an AWS CloudWatch Observability Access Manager Sink Policy.

## Basic Example

```yaml
resource:
  aws_oam_sink:
    example:
      name: ExampleSink

  aws_oam_sink_policy:
    example:
      sink_identifier: ${aws_oam_sink.example.arn}
      policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": ["oam:CreateLink", "oam:UpdateLink"] "Effect": "Allow" "Resource": "*" "Principal": { "AWS" = ["1111111111111", "222222222222"] } "Condition": { "ForAllValues:StringEquals" = { "oam:ResourceTypes" = ["AWS::CloudWatch::Metric", "AWS::Logs::LogGroup"] } } } ] }'```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `sink_identifier` - (Required) ARN of the sink to attach this policy to.
* `policy` - (Required) JSON policy to use. If you are updating an existing policy, the entire existing policy is replaced by what you specify here.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Sink.
* `sink_id` - ID string that AWS generated as part of the sink ARN.

## Timeouts

Configuration options:

* `create` - (Default `1m`)
* `update` - (Default `1m`)

## Import

```bash
ytofu import aws_oam_sink_policy.example arn:aws:oam:us-west-2:123456789012:sink/sink-id
```
