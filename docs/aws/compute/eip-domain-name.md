# Resource: aws_eip_domain_name

Assigns a static reverse DNS record to an Elastic IP addresses. See [Using reverse DNS for email applications](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html#Using_Elastic_Addressing_Reverse_DNS).

## Basic Example

```yaml
resource:
  aws_eip:
    example:
      domain: vpc

  aws_route53_record:
    example:
      zone_id: ${aws_route53_zone.main.zone_id}
      name: reverse
      type: A
      records: 
        - ${aws_eip.example.public_ip}

  aws_eip_domain_name:
    example:
      allocation_id: ${aws_eip.example.allocation_id}
      domain_name: ${aws_route53_record.example.fqdn}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `allocation_id` - (Required) The allocation ID.
* `domain_name` - (Required) The domain name to modify for the IP address.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `ptr_record` - The DNS pointer (PTR) record for the IP address.

## Timeouts

Configuration options:

- `create` - (Default `10m`)
- `update` - (Default `10m`)
- `delete` - (Default `10m`)

## Import

```bash
ytofu import aws_eip_domain_name.test eipassoc-ab12c345
```
