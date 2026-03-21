# Resource: aws_cloudwatch_dashboard

Provides a CloudWatch Dashboard resource.

## Basic Example

```yaml
resource:
  aws_cloudwatch_dashboard:
    main:
      dashboard_name: my-dashboard
      dashboard_body: '{ "widgets": [ { "type": "metric" "x": 0 "y": 0 "width": 12 "height": 6 "properties": { "metrics": [ [ "AWS/EC2", "CPUUtilization", "InstanceId", "i-012345" ] ] "period": 300 "stat": "Average" "region": "us-east-1" "title": "EC2 Instance CPU" } }, { "type": "text" "x": 0 "y": 7 "width": 3 "height": 3 "properties": { "markdown": "Hello world" } } ] }'
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `dashboard_name` - (Required) The name of the dashboard.
* `dashboard_body` - (Required) The detailed information about the dashboard, including what widgets are included and their location on the dashboard. You can read more about the body structure in the [documentation](https://docs.aws.amazon.com/AmazonCloudWatch/latest/APIReference/CloudWatch-Dashboard-Body-Structure.html).

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `dashboard_arn` - The Amazon Resource Name (ARN) of the dashboard.

## Import

```bash
ytofu import aws_cloudwatch_dashboard.sample dashboard_name
```
