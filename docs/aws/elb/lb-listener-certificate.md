# Resource: aws_lb_listener_certificate

Provides a Load Balancer Listener Certificate resource.

## Basic Example

```yaml
resource:
  aws_acm_certificate:
    example:

  aws_lb:
    front_end:

  aws_lb_listener:
    front_end:

  aws_lb_listener_certificate:
    example:
      listener_arn: ${aws_lb_listener.front_end.arn}
      certificate_arn: ${aws_acm_certificate.example.arn}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `listener_arn` - (Required, Forces New Resource) The ARN of the listener to which to attach the certificate.
* `certificate_arn` - (Required, Forces New Resource) The ARN of the certificate to attach to the listener.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The `listener_arn` and `certificate_arn` separated by a `_`.

## Import

```bash
ytofu import aws_lb_listener_certificate.example arn:aws:elasticloadbalancing:us-west-2:123456789012:listener/app/test/8e4497da625e2d8a/9ab28ade35828f96/67b3d2d36dd7c26b_arn:aws:iam::123456789012:server-certificate/tf-acc-test-6453083910015726063
```
