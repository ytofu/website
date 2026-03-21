# Resource: aws_wafregional_ipset

Provides a WAF Regional IPSet Resource for use with Application Load Balancer.

## Basic Example

```yaml
resource:
  aws_wafregional_ipset:
    ipset:
      name: tfIPSet
      ip_set_descriptor:
        type: IPV4
        value: 192.0.7.0/24
      ip_set_descriptor:
        type: IPV4
        value: 10.16.16.0/16
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name or description of the IPSet.
* `ip_set_descriptor` - (Optional) One or more pairs specifying the IP address type (IPV4 or IPV6) and the IP address range (in CIDR notation) from which web requests originate.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the WAF IPSet.
* `arn` - The ARN of the WAF IPSet.

## Import

```bash
ytofu import aws_wafregional_ipset.example a1b2c3d4-d5f6-7777-8888-9999aaaabbbbcccc
```
