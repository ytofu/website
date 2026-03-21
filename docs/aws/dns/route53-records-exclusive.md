# Route53 Records Exclusive

Manage Route53 Records Exclusive resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_route53_zone:
    example:
      name: example.com
      force_destroy: true

resource:
  aws_route53_records_exclusive:
    test:
      zone_id: ${aws_route53_zone.test.zone_id}
      resource_record_set:
        name: subdomain.example.com
        type: A
        ttl: 30
        resource_records:
          value: 127.0.0.1
        resource_records:
          value: 127.0.0.27
```

## Disallow Record Sets

```yaml
resource:
  aws_route53_records_exclusive:
    test:
      zone_id: ${aws_route53_zone.test.zone_id}
```
