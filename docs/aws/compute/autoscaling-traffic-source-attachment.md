# Resource: aws_autoscaling_traffic_source_attachment

Attaches a traffic source to an Auto Scaling group.

## Basic Example

```yaml
resource:
  aws_autoscaling_traffic_source_attachment:
    example:
      autoscaling_group_name: ${aws_autoscaling_group.example.id}
      traffic_source:
        identifier: ${aws_lb_target_group.example.arn}
        type: elbv2
```

## Argument Reference

This resource supports the following arguments:

- `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
- `autoscaling_group_name` - (Required) The name of the Auto Scaling group.
- `traffic_source` - (Required) The unique identifiers of a traffic sources.

`traffic_source` supports the following:

- `identifier` - (Required) Identifies the traffic source. For Application Load Balancers, Gateway Load Balancers, Network Load Balancers, and VPC Lattice, this will be the Amazon Resource Name (ARN) for a target group in this account and Region. For Classic Load Balancers, this will be the name of the Classic Load Balancer in this account and Region.
- `type` - (Required) Provides additional context for the value of `identifier`.
  The following lists the valid values:
  `elb` if `identifier` is the name of a Classic Load Balancer.
  `elbv2` if `identifier` is the ARN of an Application Load Balancer, Gateway Load Balancer, or Network Load Balancer target group.
  `vpc-lattice` if `identifier` is the ARN of a VPC Lattice target group.

## Attribute Reference

This resource exports no additional attributes.
