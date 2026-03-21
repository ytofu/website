# Resource: aws_rum_metrics_destination

Provides a CloudWatch RUM Metrics Destination resource.

## Basic Example

```yaml
resource:
  aws_rum_metrics_destination:
    example:
      app_monitor_name: ${aws_rum_app_monitor.example.name}
      destination: CloudWatch
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `app_monitor_name` - (Required) The name of the CloudWatch RUM app monitor that will send the metrics.
* `destination` - (Required)  Defines the destination to send the metrics to. Valid values are `CloudWatch` and `Evidently`. If you specify `Evidently`, you must also specify the ARN of the CloudWatchEvidently experiment that is to be the destination and an IAM role that has permission to write to the experiment.
* `destination_arn` - (Optional) Use this parameter only if Destination is Evidently. This parameter specifies the ARN of the Evidently experiment that will receive the extended metrics.
* `iam_role_arn` - (Optional) This parameter is required if Destination is Evidently. If Destination is CloudWatch, do not use this parameter.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The name of the CloudWatch RUM app monitor that will send the metrics.

## Import

```bash
ytofu import aws_rum_metrics_destination.example example
```
