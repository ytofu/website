# Resource: aws_oam_sink

ytofu resource for managing an AWS CloudWatch Observability Access Manager Sink.

## Basic Example

```yaml
resource:
  aws_oam_sink:
    example:
      name: ExampleSink
      tags:
        Env: prod
```

## Argument Reference

The following arguments are required:

* `name` - (Required) Name for the sink.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Sink.
* `id` - ARN of the Sink. Use `arn` instead.
* `sink_id` - ID string that AWS generated as part of the sink ARN.

## Timeouts

Configuration options:

* `create` - (Default `1m`)
* `update` - (Default `1m`)
* `delete` - (Default `1m`)

## Import

```bash
ytofu import aws_oam_sink.example arn:aws:oam:us-west-2:123456789012:sink/sink-id
```
