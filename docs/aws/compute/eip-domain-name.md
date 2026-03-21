# EIP Domain Name

Manage EIP Domain Name resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_eip:
    example:
      domain: vpc

resource:
  aws_route53_record:
    example:
      zone_id: ${aws_route53_zone.main.zone_id}
      name: reverse
      type: A
      records: 
        - ${aws_eip.example.public_ip}

resource:
  aws_eip_domain_name:
    example:
      allocation_id: ${aws_eip.example.allocation_id}
      domain_name: ${aws_route53_record.example.fqdn}
```
