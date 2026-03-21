# Resource: aws_autoscaling_lifecycle_hook

Provides an AutoScaling Lifecycle Hook resource.

## Basic Example

```yaml
resource:
  aws_autoscaling_group:
    foobar:
      availability_zones: 
        - us-west-2a
      name: terraform-test-foobar5
      health_check_type: EC2
      termination_policies: 
        - OldestInstance
      tag:
        key: Foo
        value: foo-bar
        propagate_at_launch: true

resource:
  aws_autoscaling_lifecycle_hook:
    foobar:
      name: foobar
      autoscaling_group_name: ${aws_autoscaling_group.foobar.name}
      default_result: CONTINUE
      heartbeat_timeout: 2000
      lifecycle_transition: "autoscaling:EC2_INSTANCE_LAUNCHING"
      notification_metadata: '{ "foo": "bar" }'
      notification_target_arn: "arn:aws:sqs:us-east-1:444455556666:queue1*"
      role_arn: "arn:aws:iam::123456789012:role/S3Access"
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) Name of the lifecycle hook.
* `autoscaling_group_name` - (Required) Name of the Auto Scaling group to which you want to assign the lifecycle hook
* `default_result` - (Optional) Defines the action the Auto Scaling group should take when the lifecycle hook timeout elapses or if an unexpected failure occurs. The value for this parameter can be either CONTINUE or ABANDON. The default value for this parameter is ABANDON.
* `heartbeat_timeout` - (Optional) Defines the amount of time, in seconds, that can elapse before the lifecycle hook times out. When the lifecycle hook times out, Auto Scaling performs the action defined in the DefaultResult parameter
* `lifecycle_transition` - (Required) Instance state to which you want to attach the lifecycle hook. For a list of lifecycle hook types, see [describe-lifecycle-hook-types](https://docs.aws.amazon.com/cli/latest/reference/autoscaling/describe-lifecycle-hook-types.html#examples)
* `notification_metadata` - (Optional) Contains additional information that you want to include any time Auto Scaling sends a message to the notification target.
* `notification_target_arn` - (Optional) ARN of the notification target that Auto Scaling will use to notify you when an instance is in the transition state for the lifecycle hook. This ARN target can be either an SQS queue, an SNS topic, or a Lambda function.
* `role_arn` - (Optional) ARN of the IAM role that allows the Auto Scaling group to publish to the specified notification target.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_autoscaling_lifecycle_hook.test-lifecycle-hook asg-name/lifecycle-hook-name
```
