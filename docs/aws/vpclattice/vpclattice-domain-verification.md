# Vpclattice Domain Verification

Manage Vpclattice Domain Verification resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpclattice_domain_verification:
    example:
      domain_name: example.com

resource:
  aws_route53_record:
    example:
      zone_id: ${aws_route53_zone.example.zone_id}
      name: ${aws_vpclattice_domain_verification.example.txt_record_name}
      type: TXT
      ttl: 300
      records: 
        - ${aws_vpclattice_domain_verification.example.txt_record_value}
```

## With Tags

```yaml
resource:
  aws_vpclattice_domain_verification:
    example:
      domain_name: example.com
      tags:
        Environment: production
        Purpose: domain-verification
```
