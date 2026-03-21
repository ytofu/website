# Resource: aws_elb_attachment

Attaches an EC2 instance to an Elastic Load Balancer (ELB). For attaching resources with Application Load Balancer (ALB) or Network Load Balancer (NLB), see the `aws_lb_target_group_attachment` resource.

## Basic Example

```yaml
resource:
  aws_elb_attachment:
    baz:
      elb: ${aws_elb.bar.id}
      instance: ${aws_instance.foo.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `elb` - (Required) The name of the ELB.
* `instance` - (Required) Instance ID to place in the ELB pool.

## Attribute Reference

This resource exports no additional attributes.
