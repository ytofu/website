# Resource: aws_autoscaling_attachment

Attaches a load balancer to an Auto Scaling group.

## Basic Example

```yaml
resource:
  aws_autoscaling_attachment:
    example:
      autoscaling_group_name: ${aws_autoscaling_group.example.id}
      elb: ${aws_elb.example.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `autoscaling_group_name` - (Required) Name of ASG to associate with the ELB.
* `elb` - (Optional) Name of the ELB.
* `lb_target_group_arn` - (Optional) ARN of a load balancer target group.

## Attribute Reference

This resource exports no additional attributes.
