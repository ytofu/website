# Resource: aws_cloudwatch_log_stream

Provides a CloudWatch Log Stream resource.

## Basic Example

```yaml
resource:
  aws_cloudwatch_log_group:
    yada:
      name: Yada

  aws_cloudwatch_log_stream:
    foo:
      name: SampleLogStream1234
      log_group_name: ${aws_cloudwatch_log_group.yada.name}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name of the log stream. Must not be longer than 512 characters and must not contain `:`
* `log_group_name` - (Required) The name of the log group under which the log stream is to be created.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The Amazon Resource Name (ARN) specifying the log stream.

## Import

```bash
ytofu import aws_cloudwatch_log_stream.foo Yada:SampleLogStream1234
```
