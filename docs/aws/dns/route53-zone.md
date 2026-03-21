# Route53 Zone

Manage Route53 Zone resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_route53_zone:
    primary:
      name: example.com
```

## Public Subdomain Zone

```yaml
resource:
  aws_route53_zone:
    main:
      name: example.com

resource:
  aws_route53_zone:
    dev:
      name: dev.example.com
      tags:
        Environment: dev

resource:
  aws_route53_record:
    dev-ns:
      zone_id: ${aws_route53_zone.main.zone_id}
      name: dev.example.com
      type: NS
      ttl: 30
      records: ${aws_route53_zone.dev.name_servers}
```

## Private Zone

```yaml
resource:
  aws_vpc:
    primary:
      cidr_block: 10.6.0.0/16
      enable_dns_hostnames: true
      enable_dns_support: true

resource:
  aws_vpc:
    secondary:
      cidr_block: 10.7.0.0/16
      enable_dns_hostnames: true
      enable_dns_support: true

resource:
  aws_route53_zone:
    private:
      name: example.com
      vpc:
        vpc_id: ${aws_vpc.primary.id}
      vpc:
        vpc_id: ${aws_vpc.secondary.id}
```
