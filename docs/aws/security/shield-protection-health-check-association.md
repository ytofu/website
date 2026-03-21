# Resource: aws_shield_protection_health_check_association

Creates an association between a Route53 Health Check and a Shield Advanced protected resource.
This association uses the health of your applications to improve responsiveness and accuracy in attack detection and mitigation.

## Basic Example

```yaml
data:
  aws_region:
    current:

  aws_caller_identity:
    current:

  aws_partition:
    current:

resource:
  aws_eip:
    example:
      domain: vpc
      tags:
        Name: example

  aws_shield_protection:
    example:
      name: example-protection
      resource_arn: "arn:${data.aws_partition.current.partition}:ec2:${data.aws_region.current.region}:${data.aws_caller_identity.current.account_id}:eip-allocation/${aws_eip.example.id}"

  aws_route53_health_check:
    example:
      ip_address: ${aws_eip.example.public_ip}
      port: 80
      type: HTTP
      resource_path: /ready
      failure_threshold: 3
      request_interval: 30
      tags:
        Name: tf-example-health-check

  aws_shield_protection_health_check_association:
    example:
      health_check_arn: ${aws_route53_health_check.example.arn}
      shield_protection_id: ${aws_shield_protection.example.id}```

## Argument Reference

This resource supports the following arguments:

* `health_check_arn` - (Required) The ARN (Amazon Resource Name) of the Route53 Health Check resource which will be associated to the protected resource.
* `shield_protection_id` - (Required) The ID of the protected resource.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The unique identifier (ID) for the Protection object that is created.

## Import

```bash
ytofu import aws_shield_protection_health_check_association.example ff9592dc-22f3-4e88-afa1-7b29fde9669a+arn:aws:route53:::healthcheck/3742b175-edb9-46bc-9359-f53e3b794b1b
```
